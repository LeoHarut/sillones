<!doctype html>
<html lang="es">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>Tienda de Sillones</title>
  <style>
    :root{--bg:#f6f6f6;--card:#ffffff;--accent:#2d7d46;--muted:#666;}
    *{box-sizing:border-box}
    body{font-family:Inter,system-ui,Arial,sans-serif;background:var(--bg);margin:0;color:#111}
    .site-header{display:flex;align-items:center;justify-content:space-between;padding:16px 24px;background:#fff;box-shadow:0 1px 4px rgba(0,0,0,0.05)}
    .site-header h1{margin:0;font-size:20px}
    .header-actions button{background:transparent;border:0;font-size:18px;cursor:pointer}

    .products-grid{display:grid;gap:18px;padding:24px;grid-template-columns:repeat(auto-fill,minmax(220px,1fr));max-width:1200px;margin:0 auto}
    .card{background:var(--card);border-radius:10px;box-shadow:0 6px 18px rgba(0,0,0,0.06);overflow:hidden;display:flex;flex-direction:column}
    .card img{width:100%;height:180px;object-fit:cover}
    .card-body{padding:14px;flex:1;display:flex;flex-direction:column}
    .card-title{font-weight:600;margin:0 0 8px}
    .card-desc{font-size:13px;color:var(--muted);margin-bottom:12px;flex:1}
    .card-bottom{display:flex;align-items:center;justify-content:space-between}
    .price{font-weight:700}
    .btn{padding:8px 12px;border-radius:8px;border:0;cursor:pointer}
    .btn-primary{background:var(--accent);color:#fff}

    .cart-modal{position:fixed;right:20px;top:80px;width:360px;max-width:calc(100% - 40px);background:transparent;pointer-events:none;z-index:999}
    .cart-content{pointer-events:auto;background:var(--card);padding:12px;border-radius:10px;box-shadow:0 10px 30px rgba(0,0,0,0.12)}
    .close-btn{background:transparent;border:0;font-size:20px;float:right;cursor:pointer}
    .cart-items{list-style:none;padding:0;margin:8px 0;max-height:360px;overflow:auto}
    .cart-item{display:flex;gap:10px;align-items:center;padding:8px 0;border-bottom:1px solid #f1f1f1}
    .cart-item img{width:56px;height:40px;object-fit:cover;border-radius:6px}
    .qty-control{display:flex;gap:6px;align-items:center}
    .qty-control button{padding:4px 8px;border-radius:6px;border:1px solid #ddd;background:#fff;cursor:pointer}
    .cart-footer{display:flex;align-items:center;justify-content:space-between;margin-top:12px}
    .primary{background:var(--accent);color:#fff;padding:8px 12px;border-radius:8px;border:0;cursor:pointer}

    #whatsapp-float{position:fixed;right:18px;bottom:18px;width:56px;height:56px;border-radius:50%;display:flex;align-items:center;justify-content:center;background:#25D366;box-shadow:0 6px 18px rgba(0,0,0,0.15);}
    #whatsapp-float img{width:28px;height:28px}

    @media (max-width:520px){
      .card img{height:140px}
      .cart-modal{left:10px;right:10px;top:auto;bottom:90px;width:auto}
    }
  </style>
</head>
<body>
  <header class="site-header">
    <h1>Tienda de Sillones</h1>
    <div class="header-actions">
      <button id="cart-btn" aria-label="Ver carrito">🛒 <span id="cart-count">0</span></button>
    </div>
  </header>

  <main>
    <section class="products-grid" id="products-grid"></section>
  </main>

  <aside id="cart-modal" class="cart-modal" aria-hidden="true" role="dialog" aria-labelledby="cart-title">
    <div class="cart-content">
      <button id="close-cart" class="close-btn" aria-label="Cerrar carrito">×</button>
      <h2 id="cart-title">Tu carrito</h2>
      <ul id="cart-items" class="cart-items"></ul>
      <div class="cart-footer">
        <p>Total: <strong id="cart-total">$0</strong></p>
        <button id="checkout-btn" class="primary">Finalizar compra</button>
      </div>
    </div>
  </aside>

  <a id="whatsapp-float" href="https://wa.me/5491164593377" target="_blank" aria-label="Chatear por WhatsApp">
    <img src="https://cdn-icons-png.flaticon.com/512/733/733585.png" alt="WhatsApp">
  </a>

  <script>
    const products = [
  {
    id: 1,
    name: "Sillón Nórdico",
    desc: "Diseño escandinavo en tela gris claro con patas de madera.",
    price: 120000,
    img: "https://images.unsplash.com/photo-1505691723518-36a5ac3be353?auto=format&fit=crop&w=600&q=80"
  },
  {
    id: 2,
    name: "Sillón Chesterfield",
    desc: "Clásico tapizado en cuero marrón, capitoné tradicional.",
    price: 180000,
    img: "https://images.unsplash.com/photo-1586023492125-27b2c045efd7?auto=format&fit=crop&w=600&q=80"
  },
  {
    id: 3,
    name: "Sillón Minimalista",
    desc: "Líneas rectas, tapizado en lino beige, estilo moderno.",
    price: 110000,
    img: "https://images.unsplash.com/photo-1616627984603-241fa14a0e43?auto=format&fit=crop&w=600&q=80"
  },
  {
    id: 4,
    name: "Sillón Relax Reclinable",
    desc: "Máximo confort, reclinable con apoyapiés integrado.",
    price: 150000,
    img: "https://images.unsplash.com/photo-1615874959474-d60942f6f3c1?auto=format&fit=crop&w=600&q=80"
  },
  {
    id: 5,
    name: "Sillón Vintage",
    desc: "Diseño retro en terciopelo mostaza con estructura metálica.",
    price: 135000,
    img: "https://images.unsplash.com/photo-1616627566859-5b38bb7a1ad6?auto=format&fit=crop&w=600&q=80"
  },
  {
    id: 6,
    name: "Sillón de Esquina",
    desc: "Sillón en L para sala amplia, en tela gris oscuro.",
    price: 250000,
    img: "https://images.unsplash.com/photo-1600607687939-ce8a6c25118c?auto=format&fit=crop&w=600&q=80"
  },
  {
    id: 7,
    name: "Sillón Individual",
    desc: "Perfecto para lectura, tapizado en azul profundo.",
    price: 95000,
    img: "https://images.unsplash.com/photo-1550258987-190a2d41a8ba?auto=format&fit=crop&w=600&q=80"
  },
  {
    id: 8,
    name: "Sillón Modular",
    desc: "Secciones modulares combinables, estilo versátil.",
    price: 270000,
    img: "https://images.unsplash.com/photo-1600585154340-be6161a56a0c?auto=format&fit=crop&w=600&q=80"
  },
  {
    id: 9,
    name: "Sillón Industrial",
    desc: "Estructura de acero con cuero envejecido.",
    price: 145000,
    img: "https://images.unsplash.com/photo-1600607687920-4d5d6c6ef91d?auto=format&fit=crop&w=600&q=80"
  },
  {
    id: 10,
    name: "Sillón Seccional",
    desc: "Amplio y cómodo, tapizado en gris topo.",
    price: 290000,
    img: "https://images.unsplash.com/photo-1600573472591-ee6c8e695a5f?auto=format&fit=crop&w=600&q=80"
  },
  {
    id: 11,
    name: "Sillón Escandinavo",
    desc: "Minimalista en tela blanca con patas de madera clara.",
    price: 125000,
    img: "https://images.unsplash.com/photo-1582582425145-ef3a5fc0a9a3?auto=format&fit=crop&w=600&q=80"
  },
  {
    id: 12,
    name: "Sillón Redondo",
    desc: "Diseño circular, ideal para espacios modernos.",
    price: 160000,
    img: "https://images.unsplash.com/photo-1598300056486-10d88d1d4a4c?auto=format&fit=crop&w=600&q=80"
  },
  {
    id: 13,
    name: "Sillón de Cuero Negro",
    desc: "Elegante y resistente, ideal para oficina o living.",
    price: 175000,
    img: "https://images.unsplash.com/photo-1585559604811-1c5c95d2a52d?auto=format&fit=crop&w=600&q=80"
  },
  {
    id: 14,
    name: "Sillón Esquinero Premium",
    desc: "Gran capacidad, diseño en L con tela de lujo.",
    price: 320000,
    img: "https://images.unsplash.com/photo-1600607687644-9d5e6487e993?auto=format&fit=crop&w=600&q=80"
  }
];

    const grid=document.getElementById('products-grid');
    const cartBtn=document.getElementById('cart-btn');
    const cartModal=document.getElementById('cart-modal');
    const closeCart=document.getElementById('close-cart');
    const cartItems=document.getElementById('cart-items');
    const cartTotal=document.getElementById('cart-total');
    const cartCount=document.getElementById('cart-count');
    const checkoutBtn=document.getElementById('checkout-btn');

    const formatPrice = (value) =>
      new Intl.NumberFormat("es-AR", { style: "currency", currency: "ARS" }).format(value);

    let cart = JSON.parse(localStorage.getItem("cart")) || [];

    function renderProducts(){
      grid.innerHTML=products.map(p=>`
        <div class="card">
          <img src="${p.img}" alt="${p.name}">
          <div class="card-body">
            <h3 class="card-title">${p.name}</h3>
            <p class="card-desc">${p.desc}</p>
            <div class="card-bottom">
              <span class="price">${formatPrice(p.price)}</span>
              <button class="btn btn-primary add-btn" data-id="${p.id}">Agregar</button>
            </div>
          </div>
        </div>
      `).join('');
    }

    function renderCart(){
      cartItems.innerHTML=cart.map(i=>`
        <li class="cart-item">
          <img src="${i.img}" alt="${i.name}">
          <div style="flex:1">
            <strong>${i.name}</strong><br>
            ${formatPrice(i.price)}
          </div>
          <div class="qty-control">
            <button aria-label="Reducir cantidad" data-id="${i.id}" data-action="decrease">-</button>
            <span>${i.qty}</span>
            <button aria-label="Aumentar cantidad" data-id="${i.id}" data-action="increase">+</button>
          </div>
        </li>
      `).join('');
      const total=cart.reduce((s,i)=>s+i.price*i.qty,0);
      cartTotal.textContent=formatPrice(total);
      cartCount.textContent=cart.reduce((s,i)=>s+i.qty,0);
      localStorage.setItem("cart", JSON.stringify(cart));
    }

    function addToCart(id){
      const item=cart.find(i=>i.id===id);
      if(item){item.qty++;}else{
        const product=products.find(p=>p.id===id);
        cart.push({...product,qty:1});
      }
      renderCart();
    }

    function changeQty(id,delta){
      const item=cart.find(i=>i.id===id);
      if(item){
        item.qty+=delta;
        if(item.qty<=0) cart=cart.filter(i=>i.id!==id);
      }
      renderCart();
    }

    // Delegación de eventos
    grid.addEventListener("click", e=>{
      if(e.target.classList.contains("add-btn")){
        addToCart(+e.target.dataset.id);
      }
    });

    cartItems.addEventListener("click", e=>{
      const btn=e.target.closest("button");
      if(!btn) return;
      const id=+btn.dataset.id;
      changeQty(id, btn.dataset.action==="increase"?1:-1);
    });

    // Modal
    cartBtn.onclick=()=>{
      cartModal.style.display='block';
      cartModal.setAttribute('aria-hidden','false');
      closeCart.focus();
    };
    closeCart.onclick=()=>{
      cartModal.style.display='none';
      cartModal.setAttribute('aria-hidden','true');
      cartBtn.focus();
    };
    document.addEventListener("keydown", e=>{
      if(e.key==="Escape" && cartModal.getAttribute("aria-hidden")==="false"){
        closeCart.click();
      }
    });

    checkoutBtn.onclick=()=>{
      if(cart.length===0){alert('Tu carrito está vacío');return;}
      const msg=cart.map(i=>`${i.name} x${i.qty}`).join('%0A');
      window.open(`https://wa.me/5491164593377?text=Hola! Quiero comprar:%0A${msg}`,'_blank');
    };

    renderProducts();
    renderCart();
  </script>
</body>
</html>
