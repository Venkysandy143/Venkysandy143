<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Vizag Hotels Booking</title>
    <style>
        /* General Styles */
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }
        header, footer {
            background-color: #333;
            color: #fff;
            text-align: center;
            padding: 20px;
        }
        .container {
            padding: 20px;
        }
        /* Hotel List Styles */
        .hotel-list {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 20px;
        }
        .hotel-item {
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
            text-align: center;
        }
        .hotel-item img {
            width: 100%;
            height: 200px;
            border-radius: 10px;
            object-fit: cover;
        }
        .hotel-item h3 {
            margin-top: 15px;
            font-size: 20px;
        }
        .hotel-item p {
            font-size: 14px;
            margin: 10px 0;
        }
        .hotel-item .price {
            font-size: 18px;
            color: green;
        }
        .booking-button {
            background-color: #4CAF50;
            color: white;
            padding: 10px;
            text-decoration: none;
            border-radius: 5px;
            cursor: pointer;
        }
        /* Booking Form Styles */
        .booking-form {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            justify-content: center;
            align-items: center;
        }
        .booking-form-content {
            background-color: #fff;
            padding: 20px;
            border-radius: 10px;
            width: 500px;
            max-width: 90%;
        }
        .booking-form h2 {
            margin-bottom: 20px;
            font-size: 24px;
            text-align: center;
        }
        .booking-form .form-group {
            margin-bottom: 15px;
        }
        .booking-form label {
            display: block;
            margin-bottom: 5px;
        }
        .booking-form input,
        .booking-form select {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
        .booking-form input[type="submit"] {
            background-color: #4CAF50;
            color: white;
            border: none;
            cursor: pointer;
        }
        .booking-form input[type="submit"]:hover {
            background-color: #45a049;
        }
        .close-button {
            background-color: red;
            color: white;
            padding: 5px 10px;
            text-decoration: none;
            border-radius: 5px;
            float: right;
            cursor: pointer;
        }
        @media (max-width: 768px) {
            .hotel-list {
                grid-template-columns: 1fr;
            }
        }

        /* Confirmation message styling */
        .confirmation-message {
            display: none;
            text-align: center;
        }
    </style>
</head>
<body>

<header>
    <h1>Welcome to Vizag Hotel Booking</h1>
    <p>Find the best hotels near Visakhapatnam for your stay</p>
</header>

<div class="container">
    <div class="hotel-list">
        <div class="hotel-item">
            <img src="hotel1.jpg" alt="The Park Visakhapatnam">
            <h3>The Park Visakhapatnam</h3>
            <p>Located by the scenic coastline, The Park offers luxury accommodations and a spa.</p>
            <p class="price">Price: ₹5,000 per night</p>
            <button class="booking-button" onclick="openBookingForm('The Park Visakhapatnam')">View Details</button>
        </div>

        <div class="hotel-item">
            <img src="hotel2.jpg" alt="Novotel Vizag">
            <h3>Novotel Vizag</h3>
            <p>Enjoy a modern stay at Novotel, overlooking the ocean and offering premium amenities.</p>
            <p class="price">Price: ₹6,500 per night</p>
            <button class="booking-button" onclick="openBookingForm('Novotel Vizag')">View Details</button>
        </div>

        <div class="hotel-item">
            <img src="hotel3.jpg" alt="WelcomHotel Grand Bay">
            <h3>WelcomHotel Grand Bay</h3>
            <p>Experience luxury and comfort at WelcomHotel with easy access to the beach.</p>
            <p class="price">Price: ₹4,200 per night</p>
            <button class="booking-button" onclick="openBookingForm('WelcomHotel Grand Bay')">View Details</button>
        </div>
    </div>
</div>

<!-- Booking Form Modal -->
<div class="booking-form" id="bookingForm">
    <div class="booking-form-content">
        <span class="close-button" onclick="closeBookingForm()">X</span>
        <h2>Booking Details for <span id="hotelName"></span></h2>
        <form id="bookingFormSubmit">
            <input type="hidden" id="hotelInput" name="hotel" value="">
            <div class="form-group">
                <label for="name">Full Name:</label>
                <input type="text" id="name" name="name" required>
            </div>
            <div class="form-group">
                <label for="email">Email Address:</label>
                <input type="email" id="email" name="email" required>
            </div>
            <div class="form-group">
                <label for="checkin">Check-In Date:</label>
                <input type="date" id="checkin" name="checkin" required>
            </div>
            <div class="form-group">
                <label for="checkout">Check-Out Date:</label>
                <input type="date" id="checkout" name="checkout" required>
            </div>
            <div class="form-group">
                <label for="rooms">Number of Rooms:</label>
                <input type="number" id="rooms" name="rooms" min="1" required>
            </div>
            <div class="form-group">
                <label for="guests">Number of Guests per Room:</label>
                <input type="number" id="guests" name="guests" min="1" required>
            </div>
            <div class="form-group">
                <label for="roomType">Room Type:</label>
                <select id="roomType" name="roomType" required>
                    <option value="single">Single Room</option>
                    <option value="double">Double Room</option>
                    <option value="suite">Suite</option>
                </select>
            </div>
            <div class="form-group">
                <input type="submit" value="Confirm Booking">
            </div>
        </form>
    </div>
</div>

<!-- Confirmation Message -->
<div class="confirmation-message" id="confirmationMessage">
    <h2>Booking Confirmed!</h2>
    <p>Thank you for your booking at <span id="confirmedHotelName"></span>.</p>
    <p>We have sent a confirmation to your email.</p>
</div>

<footer>
    <p>&copy; 2024 Vizag Hotel Booking. All rights reserved.</p>
</footer>

<script>
    // Function to open the booking form
    function openBookingForm(hotelName) {
        document.getElementById('hotelName').textContent = hotelName;
        document.getElementById('hotelInput').value = hotelName;
        document.getElementById('bookingForm').style.display = 'flex';
    }

    // Function to close the booking form
    function closeBookingForm() {
        document.getElementById('bookingForm').style.display = 'none';
    }

    // Handle form submission
    document.getElementById('bookingFormSubmit').addEventListener('submit', function(event) {
        event.preventDefault(); // Prevent actual form submission

        // Get the hotel name and display the confirmation message
        const hotelName = document.getElementById('hotelInput').value;
        document.getElementById('confirmedHotelName').textContent = hotelName;

        // Hide the booking form and show the confirmation message
        document.getElementById('bookingForm').style.display = 'none';
        document.getElementById('confirmationMessage').style.display = 'block';
    });
</script>

</body>
</html>
