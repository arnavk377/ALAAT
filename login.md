<html>
<head>
  <title>ALAAT Login Page</title>
  <style>
    /* CSS styles for the login page */
    .container {
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      height: 100vh;
    }
    h1 {
      color: #333;
    }
    input[type="text"],
    input[type="password"] {
      width: 300px;
      padding: 10px;
      margin: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
    }
    button {
      padding: 10px 20px;
      background-color: #333;
      color: #fff;
      border: none;
      border-radius: 4px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Login</h1>
    <form id="loginForm">
      <input type="text" id="usernameInput" placeholder="Username">
      <input type="password" id="passwordInput" placeholder="Password">
      <button id="loginBtn">Login</button>
    </form>
  </div>

  <script>
    // Dictionary to store username-password pairs
    var users = {
      "amay": "advani",
      "arnav": "kanekar",
      "taiyo": "iwazaki",
      "adi": "nawandhar",
      "liav": "bar"
    };
    document.addEventListener('DOMContentLoaded', function() {
      var loginForm = document.getElementById('loginForm');
      var usernameInput = document.getElementById('usernameInput');
      var passwordInput = document.getElementById('passwordInput');

      loginForm.addEventListener('submit', function(event) {
        event.preventDefault(); // Prevent form submission

        var username = usernameInput.value;
        var password = passwordInput.value;

        // Check if the username and password match
        if (users.hasOwnProperty(username) && users[username] === password) {
          window.location.href = 'https://muffinman1287.github.io/ALAAT/imagedrop.html'; // Redirect to YouTube
        } else {
          alert("Your username or password is wrong. Do better next time!");
        }
      });
    });
  </script>
</body>
</html>
