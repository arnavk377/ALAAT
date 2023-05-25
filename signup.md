<html>
<head>
  <title>ALAAT Sign Up Page</title>
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
    <h1>Sign Up</h1>
    <form id="signupForm">
      <input type="text" id="nameInput" placeholder="Name">
      <input type="text" id="uidInput" placeholder="Username">
      <input type="password" id="passwordInput" placeholder="Password">
      <button id="loginBtn">Sign Up</button>
    </form>
  </div>

  <script>
  document.getElementById("signupForm").addEventListener("submit", function(event) {
    event.preventDefault(); // Prevent form submission

    // Get the input values
    var name = document.getElementById("nameInput").value;
    var username = document.getElementById("uidInput").value;
    var password = document.getElementById("passwordInput").value;

    // Create an object with the user data
    var userData = {
      name: name,
      username: username,
      password: password
    };

    // Make the POST request
    fetch("http://alaat.duckdns.org/api/users", {
      method: "POST",
      headers: {
        "Content-Type": "application/json"
      },
      body: JSON.stringify(userData)
    })
      .then(response => response.json())
      .then(data => {
        // Handle the response data
        console.log(data); // You can do something with the response here
      })
      .catch(error => {
        // Handle any errors
        console.error(error);
      });
  });
</script>
</html>
