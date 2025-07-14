
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Stopshop</title>
  <style>
    body {
      background-color: #000;
      color: #fff;
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    .access-container {
      margin-top: 50px;
    }
    .hidden {
      display: none;
    }
    .shop-content {
      margin-top: 30px;
      width: 90%;
      max-width: 500px;
    }
    .product-image {
      max-width: 100%;
      margin-bottom: 10px;
    }
    .note {
      font-size: 0.9em;
      color: #aaa;
      text-align: center;
    }
    .countdown {
      position: fixed;
      top: 10px;
      right: 10px;
      background: #111;
      padding: 8px 12px;
      border-radius: 8px;
      font-size: 0.9em;
    }
    input, select, button {
      width: 100%;
      padding: 10px;
      margin-top: 10px;
      border: none;
      border-radius: 5px;
    }
    button {
      background-color: #333;
      color: white;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div class="countdown" id="countdown"></div>

  <div class="access-container" id="access-container">
    <h2>Enter Access Code</h2>
    <input type="text" id="access-code" placeholder="Enter your code..." />
    <button onclick="validateCode()">Enter</button>
  </div>

  <div class="shop-content hidden" id="shop-content">
    <h1>Stopshop</h1>
    <img src="sock.jpg" alt="Black Sock" class="product-image"/>
    <img src="croptop.jpg" alt="Black Crop Top" class="product-image"/>
    <p class="note">Socks come as a pair | Shop closes at 7PM</p>
    <form onsubmit="sendOrder(event)">
      <input type="number" id="crop-tops" min="2" placeholder="Number of Crop Tops (min 2)" required />
      <input type="number" id="socks" placeholder="Number of Sock Pairs" required />
      <select id="location" required>
        <option value="">Select Delivery Location</option>
        <option value="HQ">HQ</option>
        <option value="Travel Along">Travel Along</option>
      </select>
      <button type="submit">Place Order</button>
    </form>
  </div>

  <script>
    const validCode = "A10001"; // Placeholder code, can be dynamic
    function validateCode() {
      const input = document.getElementById('access-code').value;
      if (input === validCode) {
        document.getElementById('access-container').classList.add('hidden');
        document.getElementById('shop-content').classList.remove('hidden');
      } else {
        alert("Invalid code.");
      }
    }

    function countdownTo7PM() {
      const now = new Date();
      const target = new Date();
      target.setHours(19, 0, 0, 0);
      if (now > target) {
        target.setDate(target.getDate() + 1);
      }
      const diff = target - now;
      const hours = Math.floor(diff / (1000 * 60 * 60));
      const minutes = Math.floor((diff / (1000 * 60)) % 60);
      const seconds = Math.floor((diff / 1000) % 60);
      document.getElementById('countdown').textContent =
        `Closing in: ${hours}h ${minutes}m ${seconds}s`;
    }
    setInterval(countdownTo7PM, 1000);

    function sendOrder(e) {
      e.preventDefault();
      const tops = document.getElementById('crop-tops').value;
      const socks = document.getElementById('socks').value;
      const location = document.getElementById('location').value;
      const body = `Crop Tops: ${tops}%0ASocks: ${socks}%0ALocation: ${location}`;
      window.location.href = `mailto:Stopshopproduct@gmail.com?subject=New Order&body=${body}`;
    }
  </script>
</body>
</html>
