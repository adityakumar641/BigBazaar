# BigBazaar
# I Created my own website named as "Big Bazaar" both as frontend and backend. I use code as  (HTML,CSS and JavaScript)as frontend and (Node.js)as backend.
# Code:- 
<!DOCTYPE html>
<html lang="en">

<head>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BigBazaar</title>
    <script>
        document.addEventListener("DOMContentLoaded", () => {
            const productGrid = document.getElementById('product-grid');

            // Fetch and display products
            fetch('http://localhost:5000/api/products')
                .then(response => response.json())
                .then(data => {
                    console.log(data); // Check if data is logged
                    productGrid.innerHTML = ''; // Clear placeholder
                    data.forEach(product => {
                        const card = document.createElement('div');
                        card.classList.add('product-card');

                        card.innerHTML = `
                <h3>${product.name}</h3>
                <p>Price: Rs.${product.price}</p>
            `;
                        productGrid.appendChild(card);
                    });
                })


            // Form submission handling
            document.querySelector('.btn-submit').addEventListener('click', (e) => {
                e.preventDefault();

                const name = document.getElementById('name').value.trim();
                const items = document.getElementById('items').value.trim();
                const gross = parseFloat(document.getElementById('gross').value.trim());
                const discount = parseFloat(document.getElementById('discount').value.trim());
                const purchased = document.getElementById('purchased').checked;

                if (!name || !items || isNaN(gross) || isNaN(discount)) {
                    alert('Please fill in all the fields with valid data.');
                    return;
                }

                const netAmount = gross - discount;

                alert(`Customer Name: ${name}\nItems: ${items}\nGross Amount: Rs.${gross}\nDiscount: Rs.${discount}\nNet Amount: Rs.${netAmount}\nPurchased: ${purchased ? 'Yes' : 'No'}`);

                const card = document.createElement('div');
                card.classList.add('product-card');
                card.innerHTML = `
                    <h3>${items}</h3>
                    <p>Net Amount: Rs.${netAmount}</p>
                `;
                productGrid.appendChild(card);

                document.getElementById('name').value = '';
                document.getElementById('items').value = '';
                document.getElementById('gross').value = '';
                document.getElementById('discount').value = '';
                document.getElementById('purchased').checked = false;
            });

            // Burger menu toggle
            const burger = document.querySelector('.burger');
            const navbar = document.querySelector('.navbar ul');
            burger.addEventListener('click', () => {
                navbar.classList.toggle('active');
            });
        });
        // Function to add a card
        function addCard(name, price) {
            // Find the container to which the card will be added
            const productGrid = document.getElementById('product-grid');

            // Create the card element
            const card = document.createElement('div');
            card.classList.add('product-card');

            // Set the inner HTML of the card
            card.innerHTML = `
        <h3>${name}</h3>
        <p>Price: Rs.${price}</p>
    `;

            // Append the card to the product grid
            productGrid.appendChild(card);
        }

        // Example usage
        addCard('Sample Product', 500);

    </script>
    <style>
        body {
            font-family: 'Baloo Bhai';
            color: black;
            margin: 0;
            padding: 0;
            background-color: rgb(232, 111, 241);
        }

        .navbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background-color: rgb(169, 169, 237);
            padding: 10px 20px;
            position: flex;
            top: 0;
            z-index: 1000;
        }

        .navbar ul {
            list-style-type: none;

            display: flex;
            margin: 0;
            padding: 0;
            gap: 15px;

        }

        .navbar li {
            display: flex;
        }

        .navbar a {
            color: rgb(8, 37, 11);
            text-decoration: none;
            font-size: 18px;
            padding: 5px 10px;
            transition: color 0.3s ease;
        }

        .navbar a:hover {
            color: rgb(249, 248, 244);
        }

        .logo img {
            width: 120px;
            border-radius: 10px;
        }

        .burger {
            display: flex;
            flex-direction: column;
            cursor: pointer;
        }

        .burger .line {
            width: 24px;
            height: 3px;
            background-color: black;
            margin: 3px 0;
        }

        .container {
            margin: 20px auto;
            padding: 20px;
            max-width: 80%;
            background-color: white;
            border-radius: 15px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
        }

        h1 {

            text-align: center;
            background-color: #6ac16d;
            color: white;
            padding: 10px;
            border-radius: 10px;
        }

        .h2 {
            background-color: antiquewhite;
            box-sizing: border-box;
            box-shadow: inset;
        }

        .form {
            text-align: center;
            margin-top: 20px;
        }

        .form-input {
            display: block;
            width: 70%;
            margin: 10px auto;
            padding: 10px;
            font-size: 16px;
            border: 2px solid gold;
            border-radius: 10px;
        }

        .btn-submit {
            background-color: #4CAF50;
            color: white;
            border: none;
            padding: 10px 20px;
            font-size: 16px;
            cursor: pointer;
            border-radius: 8px;
            transition: background-color 0.3s ease;
        }

        .btn-submit:hover {
            background-color: rgb(20, 108, 20);
        }

        #product-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 20px;
            padding: 10px;
        }

        footer {
            text-align: center;
            margin-top: 20px;
            padding: 10px;
            background-color: purple;
            color: white;
        }

        footer a {
            color: white;
            text-decoration: none;
            font-weight: bold;
        }

        footer a:hover {
            color: rgb(119, 150, 203);
        }

        .box {
            font-size: 72px;
            text-align: center;
            background-color: red;
            color: aliceblue;
            display: none;
        }

        .product-card {
            background-color: rgb(225 204 152);
            border: 2px solid gold;
            border-radius: 10px;
            box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
            padding: 20px;
            text-align: center;
            transition: transform 0.3s ease;
        }

        .product-card:hover {
            transform: scale(1.05);
        }

        .navbar {
            flex-direction: column;
            align-items: flex-start;
        }

        .burger {
            display: flex;
        }

        .navbar ul {
            flex-direction: column;
            gap: 10px;
        }
    </style>
</head>

<body>
    <!-- Navbar -->
    <nav class="navbar">
        <div class="box" id="box-1"></div>
        <div class="box" id="box-2"></div>
        <div class="box" id="box-3"></div>
        <div class="box" id="box-4"></div>
        <ul>
            <li><a href="#">Home</a></li>
            <li><a href="#">About Us</a></li>
            <li><a href="#">Contact Us</a></li>
            <li><a href="#">Services</a></li>
        </ul>
        <div class="logo">
            <img src="https://seeklogo.com/images/B/big-bazaar-logo-3315553C03-seeklogo.com.png" alt="BigBazaar Logo">
        </div>
        <div class="burger">
            <div class="line"></div>
            <div class="line"></div>
            <div class="line"></div>
        </div>
    </nav>

    <!-- Header -->
    <h1>BigBazaar</h1>

    <!-- Form -->
    <div class="container">
        <div class="form">
            <input type="text" class="form-input" id="name" placeholder="Enter Your Name">
            <input type="text" class="form-input" id="items" placeholder="Enter Your Items">
            <input type="text" class="form-input" id="gross" placeholder="Gross Amount">
            <input type="text" class="form-input" id="discount" placeholder="Discount">
            <label>
                <input type="checkbox" id="purchased"> Purchased
            </label>
            <button type="submit" class="btn-submit">Submit</button>
        </div>
    </div>
    <div class="product-card">
        <h3>Product Name</h3>
        <p>Price: Rs. 500</p>
    </div>
    <div class="container">
        <h2>Product List</h2>
        <div id="product-grid">
            <h2>Paneer -70/-</h2>
            <h2>Butter-50/-</h2>
            <h2>Chocolates-100/-</h2>
            <h2>Milk-135/-</h2>
            <h2>Bread-35/-</h2>
            <h2>Candies-5/-</h2>
        </div>
    </div>

    <footer>
        <a href="https://www.BigBazar.com">Visit BigBazaar</a> | Copyright &copy; 2027 - All Rights Reserved
    </footer>
</body>

</html>
