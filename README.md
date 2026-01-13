<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Apni Sabzi Mandi</title>
    <style>
        body { font-family: Arial, sans-serif; margin: 0; padding: 20px; background: #f4f4f4; }
        .container { max-width: 500px; background: white; padding: 20px; border-radius: 10px; margin: auto; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
        h2 { text-align: center; color: green; }
        .item { display: flex; justify-content: space-between; align-items: center; border-bottom: 1px solid #ddd; padding: 10px 0; }
        button { background: #25D366; color: white; border: none; padding: 10px 20px; border-radius: 5px; cursor: pointer; width: 100%; font-size: 16px; margin-top: 10px; }
        input[type="number"] { width: 50px; padding: 5px; }
        .location-btn { background: #3498db; margin-bottom: 10px; }
    </style>
</head>
<body>

<div class="container">
    <h2>🥦 Apni Sabzi Mandi 🍅</h2>
    <p style="text-align:center;">8597045237</p>
    
    <div id="items-list">
        <div class="item">
            <span>Aloo (Rs.30/kg)</span>
            <input type="number" class="qty" data-name="Aloo" data-price="30" placeholder="0" min="0">
        </div>
        <div class="item">
            <span>Tamatar (Rs.40/kg)</span>
            <input type="number" class="qty" data-name="Tamatar" data-price="40" placeholder="0" min="0">
        </div>
        <div class="item">
            <span>Pyaj (Rs.50/kg)</span>
            <input type="number" class="qty" data-name="Pyaj" data-price="50" placeholder="0" min="0">
        </div>
    </div>

    <br>
    <button class="location-btn" onclick="getLocation()">📍 Get My Current Location</button>
    <p id="location-status" style="font-size: 12px; color: blue;"></p>

    <button onclick="sendOrder()">✅ Order on WhatsApp</button>
</div>

<script>
    let userLocation = "Location not shared";

    function getLocation() {
        if (navigator.geolocation) {
            navigator.geolocation.getCurrentPosition((position) => {
                userLocation = `https://www.google.com/maps?q=${position.coords.latitude},${position.coords.longitude}`;
                document.getElementById('location-status').innerText = "Location Captured! ✅";
            });
        } else {
            alert("Geolocation is not supported by this browser.");
        }
    }

    function sendOrder() {
        let items = document.querySelectorAll('.qty');
        let message = "🛒 *New Order Received!*%0A--------------------------%0A";
        let total = 0;
        let hasItems = false;

        items.forEach(item => {
            if (item.value > 0) {
                let cost = item.value * item.getAttribute('data-price');
                message += `• ${item.getAttribute('data-name')}: ${item.value}kg - Rs.${cost}%0A`;
                total += cost;
                hasItems = true;
            }
        });

        if (!hasItems) {
            alert("Kripya kam se kam ek sabzi select karein!");
            return;
        }

        message += `--------------------------%0A💰 *Total Bill: Rs.${total}*%0A📍 *Location:* ${userLocation}`;
        
        // Tumhara WhatsApp Number
        let whatsappNumber = "918597045237"; 
        window.open(`https://wa.me/${whatsappNumber}?text=${message}`, '_blank');
    }
</script>

</body>
</html>
