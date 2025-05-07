# Website-dev-Final-Project-
Website development final project: Business name Thrifted Threads - Rahul Lowada Roll no: 24120681 IIMB DBE

# Fixing the escaping issue by using simple strings outside of f-strings
from pathlib import Path
import zipfile

# Define folder structure
base_dir = Path("/mnt/data/thrifted_threads")
(base_dir / "css").mkdir(parents=True, exist_ok=True)

# CSS content
style_css = """
body {
    margin: 0;
    font-family: Arial, sans-serif;
    background: #fff;
    color: #000;
}
nav {
    background: #f5f5f5;
    padding: 10px 20px;
    display: flex;
    justify-content: space-between;
}
nav a {
    margin-left: 15px;
    text-decoration: none;
    color: #000;
}
.container {
    padding: 20px;
}
.product-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 20px;
}
.product-card {
    border: 1px solid #ddd;
    padding: 10px;
    text-align: center;
}
button {
    padding: 10px 20px;
    background: #000;
    color: #fff;
    border: none;
    cursor: pointer;
}
form input, form textarea {
    width: 100%;
    padding: 10px;
    margin-bottom: 10px;
    border: 1px solid #ccc;
}
"""

# Navigation HTML
nav_html = """
<nav>
    <div><strong>Thrifted Threads</strong></div>
    <div>
        <a href="index.html">Home</a>
        <a href="shop.html">Shop</a>
        <a href="contact.html">Contact</a>
        <a href="cart.html">Cart</a>
    </div>
</nav>
"""

# Product grid items
product_items = ""
for i in range(8):
    product_items += (
        '<div class="product-card">'
        '<img src="https://via.placeholder.com/100">'
        f'<p>Item {i+1}</p><p>$25.00</p>'
        '<button onclick="location.href=\'product.html\'">View</button>'
        '</div>'
    )

# Pages content
pages = {
    "index.html": f"""<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Home - Thrifted Threads</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
{nav_html}
<div class="container" style="text-align:center;">
    <h2>Featured Garment</h2>
    <img src="https://via.placeholder.com/200" alt="Featured" />
    <p>$30.00</p>
    <button onclick="location.href='shop.html'">SHOP</button>
</div>
</body>
</html>
""",
    "shop.html": f"""<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Shop - Thrifted Threads</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
{nav_html}
<div class="container">
    <h2>Shop</h2>
    <div class="product-grid">
        {product_items}
    </div>
</div>
</body>
</html>
""",
    "product.html": f"""<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Product - Thrifted Threads</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
{nav_html}
<div class="container" style="text-align:center;">
    <h2>Product Name</h2>
    <img src="https://via.placeholder.com/200" alt="Product" />
    <p>$25.00</p>
    <select><option>Small</option><option>Medium</option><option>Large</option></select><br><br>
    <button>Add to Cart</button>
</div>
</body>
</html>
""",
    "cart.html": f"""<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Cart - Thrifted Threads</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
{nav_html}
<div class="container">
    <h2>Your Cart</h2>
    <p>No items in cart.</p>
</div>
</body>
</html>
""",
    "contact.html": f"""<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Contact - Thrifted Threads</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
{nav_html}
<div class="container">
    <h2>Contact Us</h2>
    <form>
        <input type="text" placeholder="Name" required>
        <input type="email" placeholder="Email" required>
        <textarea placeholder="Message" required></textarea>
        <button type="submit">Send</button>
    </form>
</div>
</body>
</html>
"""
}

# Write files
(base_dir / "css" / "style.css").write_text(style_css)
for filename, content in pages.items():
    (base_dir / filename).write_text(content)

# Create ZIP archive
zip_path = "/mnt/data/thrifted_threads_site.zip"
with zipfile.ZipFile(zip_path, 'w') as zipf:
    for file in base_dir.rglob("*"):
        zipf.write(file, file.relative_to(base_dir.parent))

zip_path
