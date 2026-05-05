# 🛒 Pixel Store – GitHub-Ready Online Shop

This is a complete **multi-page HTML/CSS/JS e-commerce starter project** with:

- Product cards with prices
- Clickable product pages
- JavaScript shopping cart (localStorage)
- Dark mode toggle 🌙
- Mobile responsive layout 📱
- Pixel-art soldier boat animation 🚤

---

# 📁 PROJECT STRUCTURE

```
store-site/
│
├── index.html
├── shop.html
├── product.html
├── cart.html
│
├── css/
│   └── styles.css
│
├── js/
│   ├── products.js
│   ├── cart.js
│   └── theme.js
│
└── assets/
    └── sprite.png (optional pixel art)
```

---

# 🌐 1. PRODUCTS DATA (js/products.js)

```js
const products = [
  { id: 1, name: "Pixel Soldier", price: 10, image: "https://via.placeholder.com/150" },
  { id: 2, name: "Combat Boat", price: 25, image: "https://via.placeholder.com/150" },
  { id: 3, name: "Sniper Pack", price: 15, image: "https://via.placeholder.com/150" },
  { id: 4, name: "Elite Uniform", price: 20, image: "https://via.placeholder.com/150" }
];
```

---

# 🛒 2. CART SYSTEM (js/cart.js)

```js
let cart = JSON.parse(localStorage.getItem("cart")) || [];

function saveCart() {
  localStorage.setItem("cart", JSON.stringify(cart));
}

function addToCart(id) {
  const product = products.find(p => p.id === id);
  cart.push(product);
  saveCart();
  alert("Added to cart!");
}

function removeItem(index) {
  cart.splice(index, 1);
  saveCart();
  renderCart();
}

function renderCart() {
  const container = document.getElementById("cart");
  if (!container) return;

  container.innerHTML = cart.map((item, i) => `
    <div class="card">
      <h3>${item.name}</h3>
      <p>$${item.price}</p>
      <button onclick="removeItem(${i})">Remove</button>
    </div>
  `).join("");
}

window.onload = renderCart;
```

---

# 🌙 3. DARK MODE (js/theme.js)

```js
function toggleTheme() {
  document.body.classList.toggle("dark");

  if (document.body.classList.contains("dark")) {
    localStorage.setItem("theme", "dark");
  } else {
    localStorage.setItem("theme", "light");
  }
}

window.onload = () => {
  if (localStorage.getItem("theme") === "dark") {
    document.body.classList.add("dark");
  }
};
```

---

# 🏠 4. HOME PAGE (index.html)

```html
<!DOCTYPE html>
<html>
<head>
  <title>Pixel Store</title>
  <link rel="stylesheet" href="css/styles.css">
</head>
<body>

<header class="navbar">
  <h1>Pixel Store</h1>
  <nav>
    <a href="index.html">Home</a>
    <a href="shop.html">Shop</a>
    <a href="cart.html">Cart</a>
    <button onclick="toggleTheme()">🌙</button>
  </nav>
</header>

<section class="hero">
  <h2>Welcome to Pixel Military Store</h2>
  <p>Retro combat gear & pixel warfare aesthetics</p>
</section>

<!-- Boat Animation -->
<div class="boat-container">
  <div class="boat">
    <div class="soldier"></div>
    <div class="soldier"></div>
    <div class="soldier"></div>
  </div>
</div>

<script src="js/theme.js"></script>
</body>
</html>
```

---

# 🛍️ 5. SHOP PAGE (shop.html)

```html
<!DOCTYPE html>
<html>
<head>
  <title>Shop</title>
  <link rel="stylesheet" href="css/styles.css">
</head>
<body>

<header class="navbar">
  <h1>Shop</h1>
  <nav>
    <a href="index.html">Home</a>
    <a href="cart.html">Cart</a>
    <button onclick="toggleTheme()">🌙</button>
  </nav>
</header>

<section id="shop" class="grid"></section>

<script src="js/products.js"></script>
<script src="js/cart.js"></script>
<script src="js/theme.js"></script>

<script>
const shop = document.getElementById("shop");

shop.innerHTML = products.map(p => `
  <div class="card">
    <img src="${p.image}">
    <h3>${p.name}</h3>
    <p>$${p.price}</p>
    <button onclick="addToCart(${p.id})">Add to Cart</button>
    <a href="product.html?id=${p.id}">View</a>
  </div>
`).join("");
</script>

</body>
</html>
```

---

# 📦 6. PRODUCT PAGE (product.html)

```html
<!DOCTYPE html>
<html>
<head>
  <title>Product</title>
  <link rel="stylesheet" href="css/styles.css">
</head>
<body>

<div id="product"></div>

<script src="js/products.js"></script>
<script src="js/cart.js"></script>

<script>
const id = Number(new URLSearchParams(window.location.search).get("id"));
const product = products.find(p => p.id === id);

const container = document.getElementById("product");

container.innerHTML = `
  <div class="card large">
    <img src="${product.image}">
    <h1>${product.name}</h1>
    <p>$${product.price}</p>
    <button onclick="addToCart(${product.id})">Add to Cart</button>
  </div>
`;
</script>

</body>
</html>
```

---

# 🧺 7. CART PAGE (cart.html)

```html
<!DOCTYPE html>
<html>
<head>
  <title>Cart</title>
  <link rel="stylesheet" href="css/styles.css">
</head>
<body>

<h1>Your Cart</h1>
<div id="cart"></div>

<script src="js/products.js"></script>
<script src="js/cart.js"></script>

</body>
</html>
```

---

# 🎨 8. STYLES (css/styles.css)

```css
body {
  margin: 0;
  font-family: Arial;
  background: #0f172a;
  color: white;
}

.navbar {
  display: flex;
  justify-content: space-between;
  padding: 15px;
  background: #111;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
  gap: 20px;
  padding: 20px;
}

.card {
  background: #1e293b;
  padding: 15px;
  border-radius: 10px;
  text-align: center;
}

.card img {
  width: 100%;
}

button {
  padding: 8px;
  background: #38bdf8;
  border: none;
  cursor: pointer;
}

/* DARK MODE */
body.dark {
  background: #000;
  color: #fff;
}

/* MOBILE */
@media (max-width: 768px) {
  .grid {
    grid-template-columns: 1fr;
  }
}

/* BOAT ANIMATION */
.boat-container {
  position: fixed;
  bottom: 0;
  width: 100%;
}

.boat {
  display: flex;
  animation: move 10s linear infinite;
}

.soldier {
  width: 10px;
  height: 10px;
  background: lime;
  margin: 2px;
}

@keyframes move {
  from { transform: translateX(-200px); }
  to { transform: translateX(120vw); }
}
```

---

# 🚀 HOW TO PUT THIS ON GITHUB

1. Create repo: `pixel-store`
2. Upload all files
3. Go to Settings → Pages
4. Select `main branch`
5. Click save

Your site will appear at:

```
https://yourusername.github.io/pixel-store/
```

---

# 🔥 WHAT YOU NOW HAVE

✔ Real store layout
✔ Functional shopping cart
✔ Product system
✔ Dynamic product pages
✔ Dark mode
✔ Responsive design
✔ Animated pixel boat soldiers
✔ GitHub Pages ready

---

If you want next upgrade, I can help you add:

- Checkout page (fake or Stripe-ready)
- Better pixel sprite animations (real frame sheets)
- Category filtering
- Search bar
- Inventory system

Just tell me 👍

