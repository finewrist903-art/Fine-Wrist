<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fine Wrist</title>
    <link rel="icon" href="data:image/svg+xml;utf8,
<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 256 256'>
  <rect width='256' height='256' rx='40' fill='%23111'/>
  <path d='M48 148 Q128 60 208 148' fill='none' stroke='%23ffb86b' stroke-width='18' stroke-linecap='round'/>
  <text x='50%' y='68%' text-anchor='middle' font-family='Poppins, Arial, sans-serif' font-weight='700' font-size='84' fill='%23fff'>FW</text>
</svg>">
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        <svg xmlns="http://www.w3.org/2000/svg" width="256" height="256" viewBox="0 0 256 256" role="img" aria-label="FineWrist icon"><rect width="256" height="256" rx="40" fill="#111"/><path d="M48 148 Q128 60 208 148" fill="none" stroke="#ffb86b" stroke-width="18" stroke-linecap="round"/><text x="50%" y="68%" text-anchor="middle" font-family="Poppins, Arial, sans-serif" font-weight="700" font-size="84" fill="#fff">FW</text></svg>body {
            background-color: #f1f3f6;
        }
        
        .product-card img {
            height: 200px;
            object-fit: cover;
        }
        
        .cart-modal .modal-dialog {
            max-width: 400px;
        }
        
        .search-bar {
            max-width: 500px;
        }
        
        .category-menu {
            background: #fff;
            border-radius: 8px;
            padding: 15px;
        }
        
        .category-menu h5 {
            font-weight: bold;
        }
        
        .navbar {
            background-color: #2874f0 !important;
        }
        
        .navbar-brand span {
            color: #ffe500 !important;
        }
        
        .btn-warning {
            background-color: #fb641b;
            border: none;
        }
    </style>
</head>

<body>
    <!-- NAVBAR -->
    <nav class="navbar navbar-expand-lg navbar-dark sticky-top">
        <div class="container-fluid">
            <a class="navbar-brand fw-bold" href="#">Fine<span>Wrist</span></a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
        <span class="navbar-toggler-icon"></span>
      </button>
            <div class="collapse navbar-collapse" id="navbarNav">
                <form class="d-flex mx-auto search-bar" onsubmit="event.preventDefault(); searchProducts()">
                    <input class="form-control me-2" type="search" placeholder="Search for watches" id="searchInput">
                    <button class="btn btn-warning" type="submit">Search</button>
                </form>
                <ul class="navbar-nav ms-auto">
                    <li class="nav-item"><a class="nav-link" href="#">Home</a></li>
                    <li class="nav-item"><a class="nav-link" href="#shop">Shop</a></li>
                    <li class="nav-item"><a class="nav-link" href="#about">About</a></li>
                    <li class="nav-item"><a class="nav-link" href="#contact">Contact</a></li>
                    <li class="nav-item">
                        <button class="btn btn-warning ms-2" data-bs-toggle="modal" data-bs-target="#cartModal">
              🛒 Cart (<span id="cartCount">0</span>)
            </button>
                    </li>
                </ul>
            </div>
        </div>
    </nav>

    <!-- HERO -->
    <header class="bg-primary text-light text-center py-5">
        <h1 class="fw-bold">Welcome to Fine Wrist</h1>
        <p>Luxury & Smart Watches at Best Prices</p>
        <p>Note their is Dollar on place of Ruppes</p>
    </header>

    <!-- SHOP LAYOUT -->
    <main class="container my-5" id="shop">
        <div class="row">
            <!-- CATEGORY MENU -->
            <aside class="col-md-3 mb-4">
                <div class="category-menu shadow-sm">
                    <h5>Categories</h5>
                    <ul class="list-unstyled">
                        <li><a href="#" onclick="filterCategory('Smart')">Smart</a></li>
                        <li><a href="#" onclick="filterCategory('Luxury')">Luxury</a></li>
                        <li><a href="#" onclick="filterCategory('Vintage')">Vintage</a></li>
                        <li><a href="#" onclick="filterCategory('Sports')">Sports</a></li>
                        <li><a href="#" onclick="filterCategory('kids')">Kids</a></li>
                        <li><a href="#" onclick="filterCategory('Women)">Women</a></li>
                    </ul>
                </div>
            </aside>

            <!-- PRODUCT LIST -->
            <section class="col-md-9">
                <div class="row" id="productList"></div>
            </section>
        </div>
    </main>

    <!-- ABOUT -->
    <section class="bg-light py-5" id="about">
        <div class="container text-center">
            <h2>About Us</h2>
            <p>Fine Wrist offers a wide collection of premium and affordable watches .</p>
        </div>
    </section>

    <!-- CONTACT -->
    <section class="py-5" id="contact">
        <div class="container text-center">
            <h2>Contact Us</h2>
            <p>Email: support@finewrist.com | Phone: +91 9212734469</p>
        </div>
    </section>

    <!-- CART MODAL -->
    <div class="modal fade" id="cartModal" tabindex="-1">
        <div class="modal-dialog">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title">Your Cart</h5>
                    <button type="button" class="btn-close" data-bs-dismiss="modal"></button>
                </div>
                <div class="modal-body" id="cartItems"></div>
                <div class="modal-footer">
                    <p class="me-auto"><strong>Total: $<span id="total">0</span></strong></p>
                    <button class="btn btn-success" onclick="checkout()">Checkout</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        const products = [{
            id: 1,
            name: "Classic Leather Watch",
            price: 311,
            img: "https://images.meesho.com/images/products/417794856/lh8be_512.avif?width=512",
            category: "Luxury"
        }, {
            id: 2,
            name: "Premium Vintage",
            price: 407,
            img: "https://images.meesho.com/images/products/567113803/kicqg_512.avif?width=512",
            category: "Vintage"
        }, {
            id: 3,
            name: "Sports Digital Watch",
            price: 80,
            img: "https://images.meesho.com/images/products/224744366/fuitj_512.avif?width=512",
            category: "Sports"
        }, {
            id: 4,
            name: "Luxury Diamond Watch",
            price: 2000,
            img: "https://images.meesho.com/images/products/461417135/iujdj_512.avif?width=512",
            category: "Luxury"
        }, {
            id: 5,
            name: "T800 ultra black",
            price: 590,
            img: "https://images.meesho.com/images/products/583805082/jbnn2_512.avif?width=360",
            category: "Smart"
        }, {
            id: 6,
            name: "Keychain",
            price: 300,
            img: "https://images.meesho.com/images/products/571534788/48ui9_512.avif?width=512",
            category: "Antique"
        }, {
            id: 7,
            name: "Kids",
            price: 281,
            img: "https://images.meesho.com/images/products/371224889/vgurk_512.avif?width=512",
            category: "Kids"
        }];

        let cart = [];

        function renderProducts(listToRender = products) {
            const list = document.getElementById('productList');
            list.innerHTML = "";
            listToRender.forEach(p => {
                list.innerHTML += `
          <div class="col-md-4 mb-4">
            <div class="card product-card h-100 shadow-sm">
              <img src="${p.img}" class="card-img-top" alt="${p.name}">
              <div class="card-body text-center d-flex flex-column">
                <h6 class="card-title">${p.name}</h6>
                <p class="card-text text-success fw-bold">$${p.price}</p>
                <button class="btn btn-warning mt-auto" onclick="addToCart(${p.id})">Add to Cart</button>
              </div>
            </div>
          </div>`;
            });
        }

        function searchProducts() {
            const query = document.getElementById('searchInput').value.toLowerCase();
            const filtered = products.filter(p => p.name.toLowerCase().includes(query));
            renderProducts(filtered);
        }

        function filterCategory(cat) {
            if (cat === 'All') {
                renderProducts(products);
            } else {
                renderProducts(products.filter(p => p.category === cat));
            }
        }

        function addToCart(id) {
            const product = products.find(p => p.id === id);
            cart.push(product);
            updateCart();
        }

        function updateCart() {
            document.getElementById('cartCount').textContent = cart.length;
            const cartItems = document.getElementById('cartItems');
            cartItems.innerHTML = "";
            let total = 0;
            cart.forEach((item, index) => {
                cartItems.innerHTML += `<p>${item.name} - $${item.price} <button class='btn btn-sm btn-danger' onclick='removeFromCart(${index})'>x</button></p>`;
                total += item.price;
            });
            document.getElementById('total').textContent = total;
        }

        function removeFromCart(index) {
            cart.splice(index, 1);
            updateCart();
        }

        function checkout() {
            if (cart.length === 0) {
                alert("Your cart is empty!");
            } else {
                alert("Thank you for shopping with Fine Wrist! Your order has been placed.");
                cart = [];
                updateCart();
            }
        }

        renderProducts();
    </script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/js/bootstrap.bundle.min.js"></script>
</body>

</html>
