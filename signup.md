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
function redirect(){
window.location.href = '{{ site.baseurl }}/login.html';
}
//const resultContainer = document.getElementById("result");
  // set up base URL to make it easier to use and implement
  const url = "https://alaat.duckdns.org/api/users"

  const create_fetch = url + '/';
  const read_fetch = url + '/';
  const delete_fetch = url + '/delete';
  const patch_fetch = url + '/update';
 // const read_button = document.getElementById("read_button");
  // const criteria = document.getElementById("criteria")
  // Display a fact pair

function create_user(){
    const body = {
        name: document.getElementById("nameInput").value,
        uid: document.getElementById("uidInput").value,
        password: document.getElementById("passwordInput").value,
    };
    const requestOptions = {
        method: 'POST',
        body: JSON.stringify(body),
        mode: 'cors', // headers for cors policy
        cache: 'default', // cahe header
        credentials: 'omit', // header for credentials
        headers: {
            "content-type": "application/json",
            'Authorization': 'Bearer my-token',
        },
    };
    fetch(create_fetch, requestOptions)
      .then(response => {
        // check if errors
        if (response.status !== 200) {
          const errorMsg = 'Database create error: ' + response.status;
          console.log(errorMsg);
          const tr = document.createElement("tr");
          const td = document.createElement("td");
          td.innerHTML = errorMsg;
          tr.appendChild(td);
          resultContainer.appendChild(tr);
          return;
        }
    })
  }
</script>
</html>
