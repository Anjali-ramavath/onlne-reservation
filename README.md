<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Online Reservation System</title>

<style>
body {
    margin: 0;
    font-family: Arial;
    background: #eef2f3;
}

.container {
    width: 900px;
    margin: 40px auto;
    display: flex;
    box-shadow: 0 5px 15px rgba(0,0,0,0.2);
}

/* LEFT SIDE (only icon now) */
.left {
    width: 30%;
    background: #dcdcdc;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 60px;
}

/* RIGHT SIDE */
.right {
    width: 70%;
    background: #0f1f24;
    color: white;
    padding: 30px;
}

h2 {
    text-align: center;
    color: gold;
}

input, button {
    width: 100%;
    padding: 10px;
    margin: 8px 0;
    border: none;
    border-radius: 5px;
}

button {
    background: gold;
    cursor: pointer;
    font-weight: bold;
}

.hidden {
    display: none;
}
</style>
</head>

<body>

<div class="container">

<!-- LEFT SIDE (NO TASK 1) -->
<div class="left">
    💻
</div>

<!-- RIGHT SIDE -->
<div class="right">

    <h2>ONLINE RESERVATION SYSTEM</h2>

    <!-- LOGIN -->
    <div id="login">
        <h3>Login</h3>
        <input type="text" id="username" placeholder="Username">
        <input type="password" id="password" placeholder="Password">
        <button onclick="login()">Login</button>
    </div>

    <!-- MENU -->
    <div id="menu" class="hidden">
        <button onclick="showReservation()">Reservation</button>
        <button onclick="showCancel()">Cancel Ticket</button>
    </div>

    <!-- RESERVATION -->
    <div id="reservation" class="hidden">
        <h3>Reservation Form</h3>
        <input type="text" id="name" placeholder="Name">
        <input type="text" id="train" placeholder="Train Number">
        <input type="text" id="class" placeholder="Class Type">
        <input type="date" id="date">
        <input type="text" id="from" placeholder="From">
        <input type="text" id="to" placeholder="To">
        <button onclick="bookTicket()">Book Ticket</button>
        <p id="pnrDisplay"></p>
    </div>

    <!-- CANCEL -->
    <div id="cancel" class="hidden">
        <h3>Cancel Ticket</h3>
        <input type="text" id="pnr" placeholder="Enter PNR">
        <button onclick="cancelTicket()">Cancel</button>
        <p id="cancelMsg"></p>
    </div>

</div>

</div>

<script>
let bookings = {};

// LOGIN (allow any login for demo)
function login() {
    let user = document.getElementById("username").value;
    let pass = document.getElementById("password").value;

    if(user !== "" && pass !== "") {
        document.getElementById("login").classList.add("hidden");
        document.getElementById("menu").classList.remove("hidden");
    } else {
        alert("Enter username and password!");
    }
}

// SHOW RESERVATION
function showReservation() {
    document.getElementById("reservation").classList.remove("hidden");
    document.getElementById("cancel").classList.add("hidden");
}

// SHOW CANCEL
function showCancel() {
    document.getElementById("cancel").classList.remove("hidden");
    document.getElementById("reservation").classList.add("hidden");
}

// BOOK TICKET
function bookTicket() {
    let pnr = "PNR" + Math.floor(Math.random()*10000);

    bookings[pnr] = {
        name: document.getElementById("name").value
    };

    document.getElementById("pnrDisplay").innerText = "Your PNR: " + pnr;
}

// CANCEL TICKET
function cancelTicket() {
    let pnr = document.getElementById("pnr").value;

    if(bookings[pnr]) {
        delete bookings[pnr];
        document.getElementById("cancelMsg").innerText = "Ticket Cancelled!";
    } else {
        document.getElementById("cancelMsg").innerText = "Invalid PNR!";
    }
}
</script>

</body>
</html>
