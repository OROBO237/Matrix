<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Matrix - Earn in Naira</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      background: linear-gradient(to right, #6a0dad, #8e2de2);
      color: white;
      font-family: Arial, sans-serif;
      padding: 20px;
      text-align: center;
    }

    .container {
      max-width: 400px;
      margin: auto;
      background: rgba(0,0,0,0.2);
      padding: 20px;
      border-radius: 10px;
    }

    input, button {
      width: 100%;
      padding: 12px;
      margin: 10px 0;
      border: none;
      border-radius: 8px;
    }

    button {
      background-color: white;
      color: #6a0dad;
      font-weight: bold;
    }

    #dashboard {
      display: none;
    }
  </style>
</head>
<body>

  <h1>Matrix</h1>
  <p>Earn ₦50 per task. Minimum withdrawal: ₦1000</p>

  <div class="container" id="register">
    <h2>Register</h2>
    <input type="text" id="regName" placeholder="Enter Full Name">
    <input type="text" id="regUser" placeholder="Choose Username">
    <input type="password" id="regPass" placeholder="Create Password">
    <button onclick="register()">Register</button>
  </div>

  <div class="container" id="login">
    <h2>Login</h2>
    <input type="text" id="logUser" placeholder="Username">
    <input type="password" id="logPass" placeholder="Password">
    <button onclick="login()">Login</button>
  </div>

  <div class="container" id="dashboard">
    <h2>Welcome, <span id="userDisplay"></span></h2>
    <p>Your Balance: ₦<span id="balance">0</span></p>
    <button onclick="earn()">Complete Task (+₦50)</button>
    <button onclick="logout()">Logout</button>
  </div>

  <script>
    let users = {}; // fake database
    let currentUser = "";

    function register() {
      const name = document.getElementById('regName').value;
      const username = document.getElementById('regUser').value;
      const password = document.getElementById('regPass').value;

      if (users[username]) {
        alert("Username already exists!");
      } else {
        users[username] = { name, password, balance: 0 };
        alert("Registered! Now log in.");
      }
    }

    function login() {
      const username = document.getElementById('logUser').value;
      const password = document.getElementById('logPass').value;

      if (users[username] && users[username].password === password) {
        currentUser = username;
        showDashboard();
      } else {
        alert("Invalid login details");
      }
    }

    function showDashboard() {
      document.getElementById("register").style.display = "none";
      document.getElementById("login").style.display = "none";
      document.getElementById("dashboard").style.display = "block";

      document.getElementById("userDisplay").innerText = currentUser;
      document.getElementById("balance").innerText = users[currentUser].balance;
    }

    function earn() {
      users[currentUser].balance += 50;
      document.getElementById("balance").innerText = users[currentUser].balance;
    }

    function logout() {
      currentUser = "";
      document.getElementById("dashboard").style.display = "none";
      document.getElementById("register").style.display = "block";
      document.getElementById("login").style.display = "block";
    }
  </script>

</body>
</html>
