<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>Boutique NG_chopi_DIAMS</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <script src="https://cdn.tailwindcss.com"></script>
</head>
<body class="bg-gray-100 text-gray-900">

  <!-- HEADER -->
  <header class="flex items-center justify-between px-4 py-4 bg-white shadow">
    <h1 id="main-title" class="text-2xl font-bold text-blue-600">NG_chopi_DIAMS Boutique</h1>
    <div class="flex space-x-2">
      <!-- Language Button -->
      <button id="langBtn" class="bg-gray-200 rounded px-3 py-1 text-gray-700 font-semibold hover:bg-blue-100 focus:outline-none">
        🌐 Langue
      </button>
      <!-- Admin Button -->
      <button id="adminBtn" class="bg-yellow-400 rounded px-3 py-1 text-white font-semibold hover:bg-yellow-500 focus:outline-none">
        Admin
      </button>
      <!-- Panier -->
      <button id="cartBtn" class="relative bg-green-500 rounded px-3 py-1 text-white font-semibold hover:bg-green-600 focus:outline-none">
        Panier
        <span id="cartCount" class="absolute -top-2 -right-2 bg-red-600 text-xs rounded-full px-2 hidden">0</span>
      </button>
    </div>
  </header>

  <!-- LANGUAGE PANEL -->
  <div id="langPanel" class="fixed inset-0 bg-black bg-opacity-30 flex justify-center items-center z-50 hidden">
    <div class="bg-white rounded-lg shadow-lg p-6 w-80 text-center">
      <h2 class="text-xl font-bold mb-4">Choisissez votre langue</h2>
      <div class="space-y-2">
        <button class="lang-choice w-full py-2 rounded bg-blue-500 text-white font-semibold" data-lang="fr">Français</button>
        <button class="lang-choice w-full py-2 rounded bg-green-500 text-white font-semibold" data-lang="ln">Lingala</button>
        <button class="lang-choice w-full py-2 rounded bg-gray-700 text-white font-semibold" data-lang="en">English</button>
      </div>
      <button id="closeLangPanel" class="mt-6 text-sm text-gray-500 hover:underline">Fermer</button>
    </div>
  </div>

  <!-- ADMIN PANEL -->
  <div id="adminPanel" class="fixed inset-x-0 bottom-0 bg-white border-t-2 border-yellow-400 shadow-lg z-40 hidden">
    <div class="max-w-3xl mx-auto p-3 flex flex-col items-center space-y-2">
      <div class="flex items-center space-x-3">
        <span class="font-bold text-yellow-500">Espace Administrateur (démo)</span>
        <span class="text-sm text-gray-400">Ici tu peux gérer tes produits (fonctionnalités à développer)</span>
      </div>
      <button id="closeAdminPanel" class="text-xs text-gray-500 hover:underline">Fermer l'admin</button>
    </div>
  </div>

  <!-- CONTENU PRINCIPAL -->
  <main class="p-6 min-h-[60vh] max-w-6xl mx-auto">
    <h2 id="welcome-title" class="text-xl font-semibold mb-6">Bienvenue sur la boutique de luxe NG_chopi_DIAMS !</h2>
    <p id="welcome-text" class="mb-6">
      Découvrez nos produits de qualité à des prix imbattables. Ajoutez au panier et recevez votre commande directement via WhatsApp.
    </p>
    <!-- Zone produits -->
    <div id="products" class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-4 gap-6">
      <!-- Les produits sont injectés par JS -->
    </div>
  </main>

  <!-- PANIER PANEL -->
  <div id="cartPanel" class="fixed inset-0 bg-black bg-opacity-40 flex justify-end z-50 hidden">
    <div class="w-full max-w-md bg-white h-full shadow-lg flex flex-col">
      <div class="flex justify-between items-center p-4 border-b">
        <h2 class="font-bold text-lg" id="cart-title">Votre Panier</h2>
        <button id="closeCartPanel" class="text-gray-500 hover:text-red-700 font-bold text-xl">&times;</button>
      </div>
      <div id="cartItems" class="flex-1 overflow-y-auto p-4 space-y-4">
        <!-- Les articles du panier sont injectés ici -->
      </div>
      <div class="p-4 border-t">
        <div class="flex justify-between mb-3">
          <span id="cart-total-label">Total :</span>
          <span id="cartTotal" class="font-bold">0 FCFA</span>
        </div>
        <button id="orderBtn" class="w-full bg-green-500 text-white py-2 rounded font-semibold hover:bg-green-600">
          Commander via WhatsApp
        </button>
      </div>
    </div>
  </div>

  <!-- FORMULAIRE CLIENT (modal) -->
  <div id="clientFormPanel" class="fixed inset-0 bg-black bg-opacity-40 flex justify-center items-center z-50 hidden">
    <div class="bg-white rounded-lg shadow-lg p-6 w-80">
      <h3 class="font-bold mb-4" id="form-title">Informations pour la commande</h3>
      <form id="clientForm" class="space-y-3">
        <div>
          <label class="block text-sm" for="clientName" id="form-name-label">Nom et prénom</label>
          <input id="clientName" required class="w-full border px-2 py-1 rounded" />
        </div>
        <div>
          <label class="block text-sm" for="clientPhone" id="form-phone-label">Téléphone</label>
          <input id="clientPhone" required class="w-full border px-2 py-1 rounded" />
        </div>
        <button class="w-full bg-blue-500 text-white py-2 rounded font-semibold hover:bg-blue-600 mt-2">
          Valider la commande
        </button>
      </form>
      <button id="closeFormPanel" class="block mx-auto mt-3 text-xs text-gray-500 hover:underline">Annuler</button>
    </div>
  </div>

  <script>
    // --- PRODUITS ---
    const defaultProducts = [
      { id:1, nameFR:"Montre de luxe", nameEN:"Luxury Watch", nameLN:"Montre ya kitoko", price: 35000, image:"https://img.freepik.com/photos-gratuite/montre-luxe_1203-2149.jpg?w=400", descFR:"Montre élégante, étanche.", descEN:"Elegant, waterproof.", descLN:"Montre ya kitoko, ezalaka résistante." },
      { id:2, nameFR:"Sac à main", nameEN:"Handbag", nameLN:"Saki ya maboko", price: 25000, image:"https://img.freepik.com/photos-gratuite/sac-main-luxe_1203-2150.jpg?w=400", descFR:"Sac chic pour femme.", descEN:"Chic bag for women.", descLN:"Saki ya basi." },
      { id:3, nameFR:"Lunettes de soleil", nameEN:"Sunglasses", nameLN:"Lunete ya moi", price: 10000, image:"https://img.freepik.com/photos-gratuite/lunettes-soleil_1203-2151.jpg?w=400", descFR:"Protection UV, look tendance.", descEN:"UV protection, trendy look.", descLN:"Lunete ya kokoka na moi." },
      { id:4, nameFR:"Chaussures homme", nameEN:"Men's Shoes", nameLN:"Sapatu ya mibali", price: 20000, image:"https://img.freepik.com/photos-gratuite/chaussures-homme_1203-2152.jpg?w=400", descFR:"Confort et élégance.", descEN:"Comfort and elegance.", descLN:"Sapatu ya mibali, ya kitoko." }
    ];
    let products = [...defaultProducts];

    // --- PANIER ---
    let cart = [];

    // --- MULTILINGUE ---
    let currentLang = "fr";
    const translations = {
      fr: {
        "main-title": "NG_chopi_DIAMS Boutique",
        "welcome-title": "Bienvenue sur la boutique de luxe NG_chopi_DIAMS !",
        "welcome-text": "Découvrez nos produits de qualité à des prix imbattables. Ajoutez au panier et recevez votre commande directement via WhatsApp.",
        "cart-title": "Votre Panier",
        "cart-total-label": "Total :",
        "orderBtn": "Commander via WhatsApp",
        "form-title": "Informations pour la commande",
        "form-name-label": "Nom et prénom",
        "form-phone-label": "Téléphone",
        "form-validate": "Valider la commande",
        "form-cancel": "Annuler",
        "langBtn": "🌐 Langue",
        "adminBtn": "Admin",
        "cartBtn": "Panier"
      },
      en: {
        "main-title": "NG_chopi_DIAMS Shop",
        "welcome-title": "Welcome to NG_chopi_DIAMS luxury shop!",
        "welcome-text": "Discover our quality products at unbeatable prices. Add to cart and receive your order via WhatsApp.",
        "cart-title": "Your Cart",
        "cart-total-label": "Total:",
        "orderBtn": "Order via WhatsApp",
        "form-title": "Order Information",
        "form-name-label": "Full name",
        "form-phone-label": "Phone",
        "form-validate": "Validate order",
        "form-cancel": "Cancel",
        "langBtn": "🌐 Language",
        "adminBtn": "Admin",
        "cartBtn": "Cart"
      },
      ln: {
        "main-title": "Boutique NG_chopi_DIAMS",
        "welcome-title": "Boyei bolamu na boutique ya NG_chopi_DIAMS !",
        "welcome-text": "Talá biloko na biso ya kitoko na motuya ya kokitisa. Bakisela na panier, zua commande na WhatsApp.",
        "cart-title": "Panier na yo",
        "cart-total-label": "Total :",
        "orderBtn": "Komanda na WhatsApp",
        "form-title": "Makambo ya commande",
        "form-name-label": "Kombo mobimba",
        "form-phone-label": "Téléphone",
        "form-validate": "Valider commande",
        "form-cancel": "Koboya",
        "langBtn": "🌐 Lokota",
        "adminBtn": "Admin",
        "cartBtn": "Panier"
      }
    };

    // --- AFFICHAGE DES PRODUITS ---
    function renderProducts() {
      const html = products.map(p => `
        <div class="bg-white rounded shadow p-4 flex flex-col items-center">
          <img src="${p.image}" alt="${p['name'+currentLang.toUpperCase()]}" class="h-32 w-32 object-cover rounded mb-3"/>
          <h3 class="font-bold mb-1">${p['name'+currentLang.toUpperCase()]}</h3>
          <p class="text-gray-500 text-sm mb-2">${p['desc'+currentLang.toUpperCase()]}</p>
          <span class="mb-2 text-lg font-semibold text-blue-600">${p.price} FCFA</span>
          <button class="addToCart bg-blue-500 text-white px-3 py-1 rounded font-bold hover:bg-blue-600" data-id="${p.id}">
            + Ajouter
          </button>
        </div>
      `).join('');
      document.getElementById('products').innerHTML = html;
      document.querySelectorAll('.addToCart').forEach(btn => {
        btn.onclick = () => addToCart(parseInt(btn.dataset.id));
      });
    }

    // --- PANIER : RENDU ET ACTIONS ---
    function updateCartCount() {
      const c = cart.reduce((s, item) => s + item.qty, 0);
      const badge = document.getElementById('cartCount');
      badge.textContent = c;
      badge.classList.toggle('hidden', c === 0);
    }
    function renderCart() {
      const cartItems = document.getElementById('cartItems');
      if(cart.length === 0) {
        cartItems.innerHTML = `<p class="text-gray-500 text-center">Panier vide</p>`;
      } else {
        cartItems.innerHTML = cart.map(item => {
          const prod = products.find(p=>p.id===item.id);
          return `<div class="flex items-center justify-between">
            <div>
              <div class="font-semibold">${prod['name'+currentLang.toUpperCase()]}</div>
              <div class="text-xs text-gray-400">${prod.price} FCFA x ${item.qty}</div>
            </div>
            <div class="flex items-center space-x-1">
              <button class="decr bg-gray-200 px-2 rounded" data-id="${item.id}">-</button>
              <span>${item.qty}</span>
              <button class="incr bg-gray-200 px-2 rounded" data-id="${item.id}">+</button>
              <button class="remove bg-red-500 text-white px-2 rounded" data-id="${item.id}">&times;</button>
            </div>
          </div>`;
        }).join('');
      }
      document.getElementById('cartTotal').textContent = cartTotal() + " FCFA";
      // Actions
      document.querySelectorAll('.decr').forEach(btn => btn.onclick = ()=>changeQty(btn.dataset.id, -1));
      document.querySelectorAll('.incr').forEach(btn => btn.onclick = ()=>changeQty(btn.dataset.id, 1));
      document.querySelectorAll('.remove').forEach(btn => btn.onclick = ()=>removeFromCart(btn.dataset.id));
    }
    function cartTotal() {
      return cart.reduce((sum, item) => {
        const prod = products.find(p=>p.id===item.id);
        return sum + prod.price * item.qty;
      }, 0);
    }
    function addToCart(id) {
      const found = cart.find(i=>i.id===id);
      if(found) found.qty += 1;
      else cart.push({id, qty:1});
      updateCartCount();
      renderCart();
    }
    function changeQty(id, delta) {
      id = parseInt(id);
      const item = cart.find(i=>i.id===id);
      if(!item) return;
      item.qty += delta;
      if(item.qty <= 0) removeFromCart(id);
      updateCartCount();
      renderCart();
    }
    function removeFromCart(id) {
      id = parseInt(id);
      cart = cart.filter(i=>i.id!==id);
      updateCartCount();
      renderCart();
    }

    // --- PANELS ---
    function showPanel(panelId) {
      document.getElementById(panelId).classList.remove('hidden');
    }
    function hidePanel(panelId) {
      document.getElementById(panelId).classList.add('hidden');
    }

    // --- COMMANDER VIA WHATSAPP ---
    function openClientForm() {
      hidePanel('cartPanel');
      showPanel('clientFormPanel');
      document.getElementById('clientForm').reset();
    }
    function sendOrderByWhatsApp(e) {
      e.preventDefault();
      const name = document.getElementById('clientName').value.trim();
      const phone = document.getElementById('clientPhone').value.trim();
      if(!name || !phone) return;
      let msg = `Commande NG_chopi_DIAMS%0AClient: ${name}%0ATel: ${phone}%0A`;
      cart.forEach(item => {
        const prod = products.find(p=>p.id===item.id);
        msg += `- ${prod['name'+currentLang.toUpperCase()]} x${item.qty} : ${prod.price*item.qty} FCFA %0A`;
      });
      msg += `Total: ${cartTotal()} FCFA`;
      const whatsappUrl = `https://wa.me/243000000000?text=${msg}`;
      window.open(whatsappUrl, '_blank');
      hidePanel('clientFormPanel');
      cart = [];
      updateCartCount();
      renderCart();
    }

    // --- MULTILINGUE ---
    function setLang(lang) {
      currentLang = lang;
      for(const key in translations[lang]) {
        const el = document.getElementById(key);
        if(el) el.textContent = translations[lang][key];
      }
      renderProducts();
      renderCart();
      document.getElementById('orderBtn').textContent = translations[lang].orderBtn;
      document.getElementById('form-title').textContent = translations[lang]["form-title"];
      document.getElementById('form-name-label').textContent = translations[lang]["form-name-label"];
      document.getElementById('form-phone-label').textContent = translations[lang]["form-phone-label"];
      document.querySelector("#clientForm button[type=submit]").textContent = translations[lang]["form-validate"];
      document.getElementById('closeFormPanel').textContent = translations[lang]["form-cancel"];
      document.getElementById('langBtn').textContent = translations[lang]["langBtn"];
      document.getElementById('adminBtn').textContent = translations[lang]["adminBtn"];
      document.getElementById('cartBtn').textContent = translations[lang]["cartBtn"];
    }

    // --- EVENTS ---
    window.onload = () => {
      renderProducts();
      updateCartCount();
      renderCart();
      setLang("fr");
    };

    // Language panel
    document.getElementById('langBtn').onclick = ()=> showPanel('langPanel');
    document.getElementById('closeLangPanel').onclick = ()=> hidePanel('langPanel');
    document.getElementById('langPanel').onclick = e => { if(e.target===e.currentTarget) hidePanel('langPanel'); };
    document.querySelectorAll('.lang-choice').forEach(btn=>{
      btn.onclick = ()=>{ setLang(btn.dataset.lang); hidePanel('langPanel'); };
    });

    // Cart
    document.getElementById('cartBtn').onclick = ()=>{ renderCart(); showPanel('cartPanel'); };
    document.getElementById('closeCartPanel').onclick = ()=> hidePanel('cartPanel');
    document.getElementById('orderBtn').onclick = openClientForm;

    // Client form
    document.getElementById('clientForm').onsubmit = sendOrderByWhatsApp;
    document.getElementById('closeFormPanel').onclick = ()=> hidePanel('clientFormPanel');

    // Admin
    document.getElementById('adminBtn').onclick = ()=> showPanel('adminPanel');
    document.getElementById('closeAdminPanel').onclick = ()=> hidePanel('adminPanel');
  </script>
</body>
</html>
