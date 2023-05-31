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
         <button id="signupBtn" onclick="create_user()">Sign Up</button>
      </form>
      <button onclick="redirect()" id="LoginBtn">Login</button>
   </div>

   <script>
      function redirect() {
         window.location.href = '{{ site.baseurl }}/login.html';
      }

      const url = "http://127.0.0.1:8086/api/users/";

      function create_user() {
         const name = document.getElementById("nameInput").value;
         const uid = document.getElementById("uidInput").value;
         const password = document.getElementById("passwordInput").value;

         const body = {
            name: name,
            uid: uid,
            password: password
         };

         const requestOptions = {
            method: 'POST',
            body: JSON.stringify(body),
            mode: 'cors', // headers for cors policy
            cache: 'default', // cahe header
            credentials: 'omit', // header for credentials
            headers: {
                  "Content-Type": "application/json",
            },
         };

         fetch(url, requestOptions)
            .then(response => {
               if (response.status !== 200) {
                  const errorMsg = 'Database create error: ' + response.status;
                  console.log(errorMsg);
                  const errorContainer = document.getElementById("errorContainer");
                  const errorMessage = document.createElement("p");
                  errorMessage.textContent = errorMsg;
                  errorContainer.appendChild(errorMessage);
               } else {
                  // Handle successful signup, e.g., redirect to a success page
                  window.location.href = '{{ site.baseurl }}/login.html';
               }
            })
            .catch(error => {
               console.log('Error:', error);
            });
      }
   </script>
</body>
</html>
