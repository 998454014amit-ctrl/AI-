<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Awesome Shop</title>
    <style>
        /* Basic Reset and Layout */
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: #f8f9fa; color: #333; }
        
        /* Header Styling */
        header { background: #2c3e50; color: #fff; padding: 1.5rem 5%; display: flex; justify-content: space-between; align-items: center; }
        header h1 { font-size: 1.8rem; }
        
        /* Main Container */
        .container { display: flex; flex-wrap: wrap; padding: 2rem 5%; gap: 2rem; }
        
        /* Product Grid */
        .products { flex: 3; min-width: 300px; display: grid; grid-template-columns: repeat(auto-fill, minmax(220px, 1fr)); gap: 1.5rem; }
        .product-card { background: #fff; padding: 1.5rem; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.05); text-align: center; transition: transform 0.2s; }
        .product-card:hover { transform: translateY(-5px); }
        .product-card .placeholder-img { background: #e0e0e0; height: 150px; border-radius: 4px; margin-bottom: 1rem; display: flex; align-items: center; justify-content: center; color: #777; }
        .product-card h3 { font-size: 1.2rem; margin-bottom: 0.5rem; }
        .product-card p { color: #e74c3c; font-weight: bold; font-size: 1.1rem; margin-bottom: 1rem; }
        
        /* Buttons */
        button { background: #3498db; color: white; border: none; padding: 0.6rem 1.2rem; cursor: pointer; border-radius: 4px; font-weight: bold; transition: background 0.2s; width: 100%; }
        button:hover { background: #2980b9; }
        
        /* Shopping Cart Sidebar */
        .cart-section { flex: 1; min-width: 250px; background: #fff; padding: 1.5rem; border-radius: 8px; box-shadow: 0 4px 6px rgba(0,0,0,0.05); height: fit-content; }
        .cart-section h2 { border-bottom: 2px solid #eee; padding-bottom: 0.5rem; margin-bottom: 1rem; }
        .cart-item { display: flex; justify-content: space-between; margin-bottom: 0.8rem; font-size: 0.95rem; }
        .cart-total { font-size: 1.2rem; font-weight: bold; text-align: right; margin-top: 1.5rem; border-top: 2px solid #eee; padding-top: 1rem; }
        #checkout-btn { background: #27ae60; margin-top: 1rem; }
        #checkout-btn:hover { background: #219653; }
        .empty-cart { color: #777; font-style: italic; }
    </style>
</head>
<body>

    <header>
        <h1>My Awesome Shop</h1>
        <div class="cart-icon">🛒 Cart (<span id="cart-count">0</span>)</div>
    </header>

    <div class="container">
        <div class="products">
            <div class="product-card">
                <div class="placeholder-img">Image 1</div>
                <h3>Wireless Headphones</h3>
                <p>$59.99</p>
                <button onclick="addToCart('Wireless Headphones', 59.99)">Add to Cart</button>
            </div>
            <div class="product-card">
                <div class="placeholder-img">Image 2</div>
                <h3>Smart Watch</h3>
                <p>$129.50</p>
                <button onclick="addToCart('Smart Watch', 129.50)">Add to Cart</button>
            </div>
            <div class="product-card">
                <div class="placeholder-img">Image 3</div>
                <h3>Mechanical Keyboard</h3>
                <p>$85.00</p>
                <button onclick="addToCart('Mechanical Keyboard', 85.00)">Add to Cart</button>
            </div>
            <div class="product-card">
                <div class="placeholder-img">Image 4</div>
                <h3>Gaming Mouse</h3>
                <p>$45.00</p>
                <button onclick="addToCart('Gaming Mouse', 45.00)">Add to Cart</button>
            </div>
        </div>

        <div class="cart-section">
            <h2>Your Cart</h2>
            <div id="cart-items">
                <p class="empty-cart">Your cart is currently empty.</p>
            </div>
            <div class="cart-total">
                Total: $<span id="total-price">0.00</span>
            </div>
            <button id="checkout-btn" onclick="checkout()">Proceed to Checkout</button>
        </div>
    </div>

    <script>
        // Shopping Cart Logic
        let cart = [];
        let total = 0;

        function addToCart(productName, price) {
            cart.push({ name: productName, price: price });
            total += price;
            updateCartUI();
        }

        function updateCartUI() {
            const cartItemsContainer = document.getElementById('cart-items');
            const cartCount = document.getElementById('cart-count');
            const totalPrice = document.getElementById('total-price');

            // Clear current cart display
            cartItemsContainer.innerHTML = '';

            if (cart.length === 0) {
                cartItemsContainer.innerHTML = '<p class="empty-cart">Your cart is currently empty.</p>';
            } else {
                // Populate cart items
                cart.forEach((item) => {
                    const div = document.createElement('div');
                    div.className = 'cart-item';
                    div.innerHTML = `<span>${item.name}</span> <span>$${item.price.toFixed(2)}</span>`;
                    cartItemsContainer.appendChild(div);
                });
            }

            // Update numbers
            cartCount.innerText = cart.length;
            totalPrice.innerText = total.toFixed(2);
        }

        function checkout() {
            if (cart.length === 0) {
                alert("Your cart is empty! Add some items first.");
            } else {
                alert(`Thank you for your purchase! Your total is $${total.toFixed(2)}.`);
                // Reset cart after mock checkout
                cart = [];
                total = 0;
                updateCartUI();
            }
        }
    </script>
</body>
</html>
