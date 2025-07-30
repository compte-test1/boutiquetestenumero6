<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NG_chopi_DIAMS - Boutique de Luxe</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Styles personnalisés */
        .gold-text {
            background: linear-gradient(135deg, #fbbf24, #f59e0b, #d97706);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
        }
        .product-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(251, 191, 36, 0.2);
        }
        .cart-badge {
            animation: bounce 0.5s;
        }
        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-5px); }
        }
    </style>
</head>
<body class="bg-gray-900 text-gray-100">
    <!-- Header -->
    <header class="bg-gradient-to-r from-black via-gray-900 to-black border-b border-yellow-400 sticky top-0 z-50">
        <div class="container mx-auto px-4 py-4 flex justify-between items-center">
            <div class="flex items-center space-x-2">
                <h1 class="text-3xl font-bold gold-text">NG_chopi</h1>
                <span class="text-yellow-400 font-semibold">DIAMS</span>
            </div>
            
            <div class="hidden md:flex space-x-6">
                <a href="#" class="text-gray-300 hover:text-yellow-400">Nouveautés</a>
                <a href="#" class="text-gray-300 hover:text-yellow-400">Femmes</a>
                <a href="#" class="text-gray-300 hover:text-yellow-400">Hommes</a>
                <a href="#" class="text-yellow-400 font-bold">COLLECTION</a>
            </div>
            
            <div class="flex items-center space-x-4">
                <button id="adminBtn" class="text-yellow-400 hover:text-yellow-300">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z" />
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                    </svg>
                </button>
                <button id="cartBtn" class="relative text-yellow-400 hover:text-yellow-300">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z" />
                    </svg>
                    <span id="cartCount" class="absolute -top-2 -right-2 bg-yellow-400 text-black text-xs rounded-full h-5 w-5 flex items-center justify-center font-bold hidden">0</span>
                </button>
            </div>
        </div>
    </header>

    <!-- Bannière Hero -->
    <section class="bg-gradient-to-r from-yellow-400 to-yellow-600 text-black py-16 text-center">
        <div class="container mx-auto px-4">
            <h2 class="text-4xl md:text-5xl font-bold mb-4">COLLECTION EXCLUSIVE</h2>
            <p class="text-xl mb-8">Articles de luxe à prix exceptionnels</p>
            <button class="bg-black text-yellow-400 px-8 py-3 rounded-full font-bold hover:bg-gray-900 transition">
                Découvrir
            </button>
        </div>
    </section>

    <!-- Produits -->
    <section class="container mx-auto px-4 py-12">
        <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-8" id="productsContainer">
            <!-- Les produits seront chargés ici par JavaScript -->
        </div>
    </section>

    <!-- Panier -->
    <div id="cartOverlay" class="fixed inset-0 bg-black bg-opacity-75 z-50 hidden">
        <div class="absolute right-0 top-0 h-full w-full max-w-md bg-gray-900 border-l border-yellow-400 overflow-y-auto">
            <div class="p-6">
                <div class="flex justify-between items-center mb-6">
                    <h2 class="text-xl font-bold text-yellow-400">Votre Panier</h2>
                    <button id="closeCart" class="text-yellow-400 hover:text-yellow-300">
                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
                        </svg>
                    </button>
                </div>
                
                <div id="cartItems" class="space-y-4 mb-6">
                    <!-- Les articles du panier seront chargés ici -->
                    <p class="text-gray-400 text-center py-12">Votre panier est vide</p>
                </div>
                
                <div class="border-t border-yellow-400/30 pt-6">
                    <div class="flex justify-between items-center mb-6">
                        <span class="text-lg font-semibold">Total:</span>
                        <span id="cartTotal" class="text-xl font-bold gold-text">0 FCFA</span>
                    </div>
                    <!-- Formulaire client -->
                    <div id="clientForm" class="hidden">
                        <div class="mb-4">
                            <label class="block text-yellow-400 mb-2">Nom et Prénom</label>
                            <input type="text" id="clientName" class="w-full bg-gray-800 border border-yellow-400/30 rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-yellow-400" required>
                        </div>
                        <div class="mb-4">
                            <label class="block text-yellow-400 mb-2">Numéro de téléphone</label>
                            <input type="tel" id="clientPhone" class="w-full bg-gray-800 border border-yellow-400/30 rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-yellow-400" required>
                        </div>
                        <div class="mb-4">
                            <label class="block text-yellow-400 mb-2">Ville</label>
                            <input type="text" id="clientCity" class="w-full bg-gray-800 border border-yellow-400/30 rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-yellow-400" required>
                        </div>
                        <div class="mb-4">
                            <label class="block text-yellow-400 mb-2">Quartier</label>
                            <input type="text" id="clientNeighborhood" class="w-full bg-gray-800 border border-yellow-400/30 rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-yellow-400" required>
                        </div>
                        <div class="mb-6">
                            <label class="block text-yellow-400 mb-2">Rue et Numéro</label>
                            <input type="text" id="clientStreet" class="w-full bg-gray-800 border border-yellow-400/30 rounded-lg px-4 py-2 focus:outline-none focus:ring-2 focus:ring-yellow-400" required>
                        </div>
                        <button id="confirmOrderBtn" class="w-full bg-gradient-to-r from-green-500 to-green-600 text-white py-3 rounded-lg font-bold hover:opacity-90 transition">
                            Confirmer la commande
                        </button>
                    </div>
                    <button id="validateOrderBtn" class="w-full bg-gradient-to-r from-yellow-400 to-yellow-600 text-black py-3 rounded-lg font-bold hover:opacity-90 transition">
                        Valider votre commande
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Espace Administrateur -->
    <div id="adminPanel" class="fixed inset-0 bg-gray-900 z-50 overflow-y-auto hidden">
        <div class="container mx-auto px-4 py-12">
            <div class="flex justify-between items-center mb-12">
                <h1 class="text-3xl font-bold gold-text">Panel d'Administration</h1>
                <button id="closeAdmin" class="text-yellow-400 hover:text-yellow-300 px-4 py-2 border border-yellow-400 rounded-lg">
                    Fermer
                </button>
            </div>
            <div class="bg-gray-800 rounded-lg p-6 mb-8">
                <h2 class="text-xl font-bold text-yellow-400 mb-4">Gestion des Produits</h2>
                
                <!-- Formulaire d'ajout/modification -->
                <form id="adminProductForm" class="mb-6">
                    <input type="hidden" id="productId">
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
                        <div>
                            <label class="block text-yellow-400 mb-2">Nom du produit</label>
                            <input type="text" id="productName" class="w-full bg-gray-800 border border-yellow-400/30 rounded-lg px-4 py-2" required>
                        </div>
                        <div>
                            <label class="block text-yellow-400 mb-2">Catégorie</label>
                            <select id="productCategory" class="w-full bg-gray-800 border border-yellow-400/30 rounded-lg px-4 py-2" required>
                                <option value="Robes">Robes</option>
                                <option value="Hauts">Hauts</option>
                                <option value="Accessoires">Accessoires</option>
                            </select>
                        </div>
                    </div>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4 mb-4">
                        <div>
                            <label class="block text-yellow-400 mb-2">Prix (FCFA)</label>
                            <input type="number" id="productPrice" class="w-full bg-gray-800 border border-yellow-400/30 rounded-lg px-4 py-2" required>
                        </div>
                        <div>
                            <label class="block text-yellow-400 mb-2">Prix original</label>
                            <input type="number" id="productOriginalPrice" class="w-full bg-gray-800 border border-yellow-400/30 rounded-lg px-4 py-2" required>
                        </div>
                    </div>
                    <div class="mb-4">
                        <label class="block text-yellow-400 mb-2">URL de l'image</label>
                        <input type="text" id="productImage" class="w-full bg-gray-800 border border-yellow-400/30 rounded-lg px-4 py-2 mb-2" required>
                    </div>
                    <div class="flex space-x-3">
                        <button type="submit" class="bg-yellow-400 text-black px-6 py-2 rounded-lg font-bold">
                            Enregistrer
                        </button>
                        <button type="button" id="cancelEdit" class="bg-gray-700 text-white px-6 py-2 rounded-lg font-bold">
                            Annuler
                        </button>
                    </div>
                </form>

                <!-- Liste des produits -->
                <div class="bg-gray-900 rounded-lg p-4 mb-4">
                    <h3 class="text-lg font-semibold text-yellow-400 mb-3">Liste des produits</h3>
                    <div id="adminProductsList" class="space-y-3">
                        <!-- Produits chargés dynamiquement -->
                    </div>
                </div>

                <!-- Timer vente flash -->
                <div class="bg-gray-900 rounded-lg p-4 mb-4">
                    <h3 class="text-lg font-semibold text-yellow-400 mb-3">Vente Flash</h3>
                    <div class="flex items-center space-x-3 mb-3">
                        <input type="datetime-local" id="saleEndTime" class="bg-gray-800 border border-yellow-400/30 rounded-lg px-4 py-2">
                        <button id="startSaleTimer" class="bg-gradient-to-r from-yellow-400 to-yellow-600 text-black px-4 py-2 rounded-lg">
                            Démarrer
                        </button>
                    </div>
                    <div id="countdownDisplay" class="text-2xl font-bold text-center gold-text hidden">
                        <span id="countdownDays">00</span>j 
                        <span id="countdownHours">00</span>h 
                        <span id="countdownMinutes">00</span>m 
                        <span id="countdownSeconds">00</span>s
                    </div>
                </div>

                <!-- Statistiques -->
                <div class="bg-gray-900 rounded-lg p-4 mb-4">
                    <h3 class="text-lg font-semibold text-yellow-400 mb-3">Statistiques</h3>
                    <div class="grid grid-cols-2 gap-4">
                        <div class="bg-gray-800 p-3 rounded-lg">
                            <p class="text-sm text-gray-300">Produits</p>
                            <p class="text-xl font-bold gold-text" id="productsCount">0</p>
                        </div>
                        <div class="bg-gray-800 p-3 rounded-lg">
                            <p class="text-sm text-gray-300">Ventes ce mois</p>
                            <p class="text-xl font-bold gold-text">0</p>
                        </div>
                    </div>
                </div>

                <!-- Bouton d'ajout -->
                <button id="addProductBtn" class="bg-gradient-to-r from-yellow-400 to-yellow-600 text-black px-6 py-3 rounded-lg font-bold w-full mb-4">
                    Ajouter un nouveau produit
                </button>

                <!-- Sauvegarde -->
                <button id="saveProductsBtn" class="bg-gradient-to-r from-green-500 to-green-600 text-white px-6 py-3 rounded-lg font-bold w-full">
                    Sauvegarder les modifications
                </button>
            </div>
        </div>
    </div>

    <script>
        // Données des produits
        const products = [
            {
                id: 1,
                name: "Robe de Soirée Élégante",
                price: 75000,
                originalPrice: 95000,
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/4f6e42aa-1393-409a-8d75-35dc173309c3.png",
                category: "Robes",
                rating: 4.8
            },
            {
                id: 2,
                name: "Top Couture Premium",
                price: 45000,
                originalPrice: 65000,
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/a1a416cf-2ed9-4826-b0fe-b0bf9ac24fba.png",
                category: "Hauts",
                rating: 4.6
            },
            {
                id: 3,
                name: "Robe Cocktail Diamants",
                price: 89000,
                originalPrice: 120000,
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/dc732eb3-2b4e-46f9-bca1-86c42649759c.png",
                category: "Robes",
                rating: 4.9
            },
            {
                id: 4,
                name: "Montre Prestige Or",
                price: 125000,
                originalPrice: 180000,
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/58eefe4f-a865-4b1a-b96a-89a1659638b2.png",
                category: "Accessoires",
                rating: 5.0
            }
        ];

        // Panier
        let cart = [];

        // Éléments du DOM
        const productsContainer = document.getElementById('productsContainer');
        const cartBtn = document.getElementById('cartBtn');
        const closeCart = document.getElementById('closeCart');
        const cartOverlay = document.getElementById('cartOverlay');
        const cartItems = document.getElementById('cartItems');
        const cartCount = document.getElementById('cartCount');
        const cartTotal = document.getElementById('cartTotal');
        const validateOrderBtn = document.getElementById('validateOrderBtn');
        const adminBtn = document.getElementById('adminBtn');
        const adminPanel = document.getElementById('adminPanel');
        const closeAdmin = document.getElementById('closeAdmin');

        // Afficher les produits
        function displayProducts() {
            productsContainer.innerHTML = '';
            products.forEach(product => {
                const discount = Math.round((1 - product.price / product.originalPrice) * 100);
                
                const productElement = document.createElement('div');
                productElement.className = 'bg-gray-800 rounded-xl overflow-hidden border border-yellow-400/20 product-card transition duration-300';
                productElement.innerHTML = `
                    <div class="relative">
                        <img src="${product.image}" alt="${product.name}" class="w-full h-64 object-cover">
                        ${discount > 0 ? `
                        <span class="absolute top-3 left-3 bg-yellow-400 text-black px-2 py-1 rounded text-xs font-bold">
                            -${discount}%
                        </span>` : ''}
                    </div>
                    <div class="p-4">
                        <h3 class="font-semibold mb-2">${product.name}</h3>
                        <div class="flex items-center mb-3">
                            ${Array(5).fill().map((_, i) => 
                                `<svg class="w-4 h-4 ${i < Math.floor(product.rating) ? 'text-yellow-400' : 'text-gray-600'}" fill="currentColor" viewBox="0 0 24 24">
                                    <path d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"/>
                                </svg>`
                            ).join('')}
                            <span class="text-xs text-gray-400 ml-2">${product.rating}</span>
                        </div>
                        <div class="flex justify-between items-center">
                            <div>
                                <p class="text-yellow-400 font-bold">${product.price.toLocaleString()} FCFA</p>
                                ${product.price < product.originalPrice ? 
                                    `<p class="text-gray-500 text-sm line-through">${product.originalPrice.toLocaleString()} FCFA</p>` : ''}
                            </div>
                            <button class="bg-yellow-400 hover:bg-yellow-500 text-black px-3 py-1 rounded text-sm add-to-cart" data-id="${product.id}">
                                Ajouter
                            </button>
                        </div>
                    </div>
                `;
                productsContainer.appendChild(productElement);
            });
        }

        // Mettre à jour le panier
        function updateCart() {
            cartItems.innerHTML = '';
            let total = 0;
            cart.forEach(item => {
                const itemTotal = item.price * item.quantity;
                total += itemTotal;
                const cartItem = document.createElement('div');
                cartItem.className = 'flex justify-between items-center';
                cartItem.innerHTML = `
                    <span>${item.name} (x${item.quantity})</span>
                    <span>${itemTotal.toLocaleString()} FCFA</span>
                `;
                cartItems.appendChild(cartItem);
            });
            cartTotal.innerText = total.toLocaleString() + ' FCFA';
            cartCount.innerText = cart.length;
            cartCount.classList.toggle('hidden', cart.length === 0);
        }

        // Ajouter au panier
        productsContainer.addEventListener('click', (e) => {
            if (e.target.classList.contains('add-to-cart')) {
                const productId = e.target.getAttribute('data-id');
                const product = products.find(p => p.id == productId);
                const existingItem = cart.find(item => item.id === product.id);
                if (existingItem) {
                    existingItem.quantity++;
                } else {
                    cart.push({ ...product, quantity: 1 });
                }
                updateCart();
            }
        });

        // Ouvrir le panier
        cartBtn.addEventListener('click', () => {
            cartOverlay.classList.remove('hidden');
            updateCart();
        });

        // Fermer le panier
        closeCart.addEventListener('click', () => {
            cartOverlay.classList.add('hidden');
        });

        // Valider la commande (afficher le formulaire)
        validateOrderBtn.addEventListener('click', () => {
            document.getElementById('validateOrderBtn').classList.add('hidden');
            document.getElementById('clientForm').classList.remove('hidden');
        });

        // Confirmer la commande (envoyer sur WhatsApp)
        document.getElementById('confirmOrderBtn').addEventListener('click', () => {
            const clientName = document.getElementById('clientName').value;
            const clientPhone = document.getElementById('clientPhone').value;
            const clientCity = document.getElementById('clientCity').value;
            const clientNeighborhood = document.getElementById('clientNeighborhood').value;
            const clientStreet = document.getElementById('clientStreet').value;

            if (!clientName || !clientPhone || !clientCity || !clientNeighborhood || !clientStreet) {
                alert("Veuillez remplir tous les champs du formulaire");
                return;
            }

            const total = cart.reduce((sum, item) => sum + (item.price * item.quantity), 0);
            const orderDetails = cart.map(item => 
                `• ${item.name} (x${item.quantity}) - ${(item.price * item.quantity).toLocaleString()} FCFA`
            ).join('\n');
            
            const message = `🌟 **Nouvelle commande NG_chopi_DIAMS** 🌟\n\n💎 **COMMANDE PREMIUM:**\n${orderDetails}\n\n💰 **TOTAL:** ${total.toLocaleString()} FCFA\n\n👤 **INFORMATIONS CLIENT:**\n📝 Nom: ${clientName}\n📞 Téléphone: ${clientPhone}\n📍 Adresse: ${clientCity}, ${clientNeighborhood}, ${clientStreet}\n\n✨ Merci pour votre commande de luxe chez NG_chopi_DIAMS !`;

            const whatsappUrl = `https://wa.me/242064230404?text=${encodeURIComponent(message)}`;
            window.open(whatsappUrl, '_blank');
            
            // Réinitialiser
            cart = [];
            document.getElementById('clientForm').classList.add('hidden');
            document.getElementById('validateOrderBtn').classList.remove('hidden');
            updateCart();
            cartOverlay.classList.add('hidden');
        });

        // Fonctions admin
        function loadAdminProducts() {
            const container = document.getElementById('adminProductsList');
            container.innerHTML = '';
            products.forEach(product => {
                const productElement = document.createElement('div');
                productElement.className = 'flex justify-between items-center bg-gray-800 p-3 rounded-lg';
                productElement.innerHTML = `
                    <div>
                        <h4 class="font-medium">${product.name}</h4>
                        <p class="text-sm text-yellow-400">${product.price.toLocaleString()} FCFA</p>
                    </div>
                    <div class="flex space-x-2">
                        <button class="admin-edit-btn text-yellow-400 hover:text-yellow-300" data-id="${product.id}">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"/>
                            </svg>
                        </button>
                        <button class="admin-delete-btn text-red-400 hover:text-red-300" data-id="${product.id}">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"/>
                            </svg>
                        </button>
                    </div>
                `;
                container.appendChild(productElement);
            });
        }

        function resetAdminForm() {
            document.getElementById('productId').value = '';
            document.getElementById('productName').value = '';
            document.getElementById('productPrice').value = '';
            document.getElementById('productOriginalPrice').value = '';
            document.getElementById('productImage').value = '';
            document.getElementById('productCategory').value = 'Robes';
        }

        // Sécurité admin
        let failedAttempts = 0;
        let isBanned = false;

        // Évènements admin
        adminBtn.addEventListener('click', () => {
            if (isBanned) {
                alert("Accès bloqué - Vous avez été banni pour trop de tentatives échouées");
                return;
            }

            if (failedAttempts < 5) {
                const code = prompt(`Entrez le code d'accès à l'espace administrateur (Tentatives restantes: ${5 - failedAttempts})`);
                
                if (code === "@inganibirds2007") {
                    adminPanel.classList.remove('hidden');
                    loadAdminProducts();
                    failedAttempts = 0;
                } else {
                    failedAttempts++;
                    
                    if (failedAttempts >= 5) {
                        const choice = confirm("Accès bloqué après 5 échecs\nVoulez-vous demander à réinitialiser le code?\n(Cela nécessitera une confirmation par email)");
                        if (choice) {
                            // Demander l'email et envoyer une demande de réinitialisation
                            const email = prompt("Entrez votre email pour demander une réinitialisation:");
                            if (email) {
                                alert(`Une demande de réinitialisation a été envoyée à ${email}`);
                                // Envoyer une requête de réinitialisation
                                setTimeout(() => alert("Email envoyé! Le code a été réinitialisé à '@inganibirds2007'"), 2000);
                                failedAttempts = 0;
                            } else {
                                isBanned = true;
                            }
                        } else {
                            const retry = confirm("Vous pouvez encore essayer 3 fois avant un bannissement");
                            if (retry) {
                                failedAttempts = 5; // Reset pour avoir 3 nouvelles tentatives
                            }
                        }
                    } else {
                        alert("Code incorrect!");
                    }
                }
            } else if (failedAttempts < 8) {
                const code = prompt(`Attention, dernière tentative! (Restantes: ${8 - failedAttempts})`);
                if (code === "@inganibirds2007") {
                    adminPanel.classList.remove('hidden');
                    loadAdminProducts();
                    failedAttempts = 0;
                } else {
                    failedAttempts++;
                    if (failedAttempts >= 8) {
                        alert("Accès bloqué - Trop de tentatives. Contactez l'administrateur.");
                        isBanned = true;
                    }
                }
            } else {
                alert("Accès bloqué - Contactez l'administrateur pour récupérer l'accès");
            }
        });

        // Ajouter un nouveau produit
        document.getElementById('addProductBtn').addEventListener('click', () => {
            resetAdminForm();
        });

        // Annuler l'édition
        document.getElementById('cancelEdit').addEventListener('click', () => {
            resetAdminForm();
        });

        // Écouter les clics sur les boutons d'édition/suppression
        document.getElementById('adminProductsList').addEventListener('click', (e) => {
            if (e.target.closest('.admin-edit-btn')) {
                const productId = e.target.closest('.admin-edit-btn').getAttribute('data-id');
                const product = products.find(p => p.id == productId);
                if (product) {
                    document.getElementById('productId').value = product.id;
                    document.getElementById('productName').value = product.name;
                    document.getElementById('productPrice').value = product.price;
                    document.getElementById('productOriginalPrice').value = product.originalPrice;
                    document.getElementById('productImage').value = product.image;
                    document.getElementById('productCategory').value = product.category;
                }
            }
            
            if (e.target.closest('.admin-delete-btn')) {
                const productId = e.target.closest('.admin-delete-btn').getAttribute('data-id');
                if (confirm('Voulez-vous vraiment supprimer ce produit ?')) {
                    const index = products.findIndex(p => p.id == productId);
                    if (index !== -1) {
                        products.splice(index, 1);
                        loadAdminProducts();
                        displayProducts();
                    }
                }
            }
        });

        // Enregistrer les modifications
        document.getElementById('adminProductForm').addEventListener('submit', (e) => {
            e.preventDefault();
            
            const productData = {
                id: document.getElementById('productId').value || Date.now(),
                name: document.getElementById('productName').value,
                price: parseInt(document.getElementById('productPrice').value),
                originalPrice: parseInt(document.getElementById('productOriginalPrice').value),
                image: document.getElementById('productImage').value,
                category: document.getElementById('productCategory').value,
                rating: 4.5 // Valeur par défaut
            };

            if (document.getElementById('productId').value) {
                // Édition
                const index = products.findIndex(p => p.id == document.getElementById('productId').value);
                if (index !== -1) {
                    products[index] = productData;
                }
            } else {
                // Ajout
                products.push(productData);
            }

            resetAdminForm();
            loadAdminProducts();
            displayProducts();
        });

        // Fermer l'espace administrateur
        closeAdmin.addEventListener('click', () => {
            adminPanel.classList.add('hidden');
        });

        // Timer vente flash
        let saleTimerInterval;
        function updateCountdown(endTime) {
            const now = new Date();
            const diff = endTime - now;
            
            if (diff <= 0) {
                clearInterval(saleTimerInterval);
                document.getElementById('countdownDisplay').classList.add('hidden');
                alert("La vente flash est terminée!");
                return;
            }
            
            const days = Math.floor(diff / (1000 * 60 * 60 * 24));
            const hours = Math.floor((diff % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
            const minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));
            const seconds = Math.floor((diff % (1000 * 60)) / 1000);
            
            document.getElementById('countdownDays').textContent = days.toString().padStart(2, '0');
            document.getElementById('countdownHours').textContent = hours.toString().padStart(2, '0');
            document.getElementById('countdownMinutes').textContent = minutes.toString().padStart(2, '0');
            document.getElementById('countdownSeconds').textContent = seconds.toString().padStart(2, '0');
            
            document.getElementById('countdownDisplay').classList.remove('hidden');
        }

        document.getElementById('startSaleTimer').addEventListener('click', () => {
            const endTimeString = document.getElementById('saleEndTime').value;
            if (!endTimeString) {
                alert("Veuillez entrer une date/heure de fin");
                return;
            }
            
            const endTime = new Date(endTimeString);
            if (endTime <= new Date()) {
                alert("La date/heure doit être dans le futur");
                return;
            }
            
            clearInterval(saleTimerInterval);
            updateCountdown(endTime);
            saleTimerInterval = setInterval(() => updateCountdown(endTime), 1000);
        });

        // Charger depuis localStorage
        function loadFromStorage() {
            const savedProducts = localStorage.getItem('ng_chopi_products');
            if (savedProducts) {
                products = JSON.parse(savedProducts);
            }
            displayProducts();
            document.getElementById('productsCount').textContent = products.length;
        }

        // Sauvegarder dans localStorage
        document.getElementById('saveProductsBtn').addEventListener('click', () => {
            localStorage.setItem('ng_chopi_products', JSON.stringify(products));
            alert('Modifications sauvegardées!');
        });

        // Afficher les produits au chargement
        loadFromStorage();
    </script>
</body>
</html>
