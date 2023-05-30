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
      <input type="name" id="nameInput" placeholder="Name">
      <button id="loginBtn">Login</button>
    </form>
  </div>

  <script>
    document.addEventListener('DOMContentLoaded', function() {
      var loginForm = document.getElementById('loginForm');
      var usernameInput = document.getElementById('usernameInput');
      var passwordInput = document.getElementById('passwordInput');
      var nameInput = document.getElemebtById('nameInput');

      loginForm.addEventListener('submit', function(event) {
        event.preventDefault(); // Prevent form submission

        var username = usernameInput.value;
        var password = passwordInput.value;
        var name = nameInput.value;

        // Make the GET request to retrieve user data
        fetch("https://alaat.duckdns.org/api/users?username=" + encodeURIComponent(username))
          .then(response => response.json())
          .then(data => {
            if (data && data.username === username && data.password === password && data.name === name) {
              window.location.href = '{{ site.baseurl }}/imagedrop.html'; // Redirect to the desired page
            } else {
              alert("Your username or password is wrong. Do better next time!");
            }
          })
          .catch(error => {
            console.error(error);
            alert("An error occurred while logging in. Please try again later.");
          });
      });
    });
  </script>
</body>
</html>
