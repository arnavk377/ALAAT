<style>
.mytd {
  height: 80px;
  width: 160px;
  text-align: center;
  vertical-align: middle;
  border: 1px solid black;
}

.myth {
  border: 1px solid black;
  height: 30px;
  background-color: aliceblue;
}

.mytable1 {
  width: 85%;
  margin: auto;
  text-align: center;
  background-color: aliceblue;
  border: 1px solid black;
  border-collapse: collapse;
}

.mytable1 th {
  padding: 5px;
}

.mytable1 td {
  border: 1px solid black;
  padding: 5px;
}

.mytext {
  font-weight: bolder;
}

.mytable {
  width: 70%;
  margin: auto;
  text-align: center;
  background-color: lightgrey;
  border-radius: 20px;
}

img {
  width: 95%;
  height: auto;
  max-height: 200px;
  object-fit: contain;
}

.mytable1 p {
  text-align: center;
  margin: 10px;
}
</style>

<table class="mytable1" id="cars_table">
  <thead>
  <tr>
    <th class="myth">ID</th>
    <th class="myth">Name</th>
    <th class="myth">Like</th>
    <th class="myth"># of Likes</th>
    <th class = "myth"> image </th>
  </tr>
  </thead>
  <tbody class="mytd" id="result">
    <!-- javascript generated data -->
  </tbody>
</table>
<script>
const resultContainer = document.getElementById("result");
  const url = "http://127.0.0.1:8086/api/images/"
  const create_fetch = url + '';
  const read_fetch = url;
  const delete_fetch = url + '/';
  const update_fetch = url;
  // Load users on page entry
  read_cars();
  // Display User Table, data is fetched from Backend Database
  function read_cars() {
    // prepare fetch options
    const read_options = {
      method: 'GET', // *GET, POST, PUT, DELETE, etc.
      mode: 'cors', // no-cors, *cors, same-origin
      cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
      credentials: 'omit', // include, *same-origin, omit
      headers: {
        'Content-Type': 'application/json'
      },
    };
    // fetch the data from API
    fetch(read_fetch, read_options)
      // response is a RESTful "promise" on any successful fetch
      .then(response => {
        // check for response errors
        if (response.status !== 200) {
            const errorMsg = 'Database read error: ' + response.status;
            console.log(errorMsg);
            const tr = document.createElement("tr");
            const td = document.createElement("td");
            td.innerHTML = errorMsg;
            tr.appendChild(td);
            resultContainer.appendChild(tr);
            return;
        }
        // valid response will have json data
        response.json().then(data => {
            console.log(data);
            for (let row in data) {
              console.log(data[row]);
              add_row(data[row]);
            }
        })
    })
    // catch fetch errors (ie ACCESS to server blocked)
    .catch(err => {
      console.error(err);
      const tr = document.createElement("tr");
      const td = document.createElement("td");
      td.innerHTML = err;
      tr.appendChild(td);
      resultContainer.appendChild(tr);
    });
  }
  function like_car(image_id, num_like, image_uid, image_name) {
  const body = {
    id: image_id,
    uid: image_uid,
    name: image_name,
    likes: num_like + 1,
  };
  const requestOptions = {
    method: 'PATCH', // *GET, POST, PUT, DELETE, etc.
    mode: 'cors', // no-cors, *cors, same-origin
    cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
    credentials: 'omit', // include, *same-origin, omit
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify(body), // send the updated like count in the request body
  };
  // Fetch API call to update the like count
  fetch(update_fetch, requestOptions)
    .then(response => {
      // trap error response from Web API
      if (response.status !== 200) {
        const errorMsg = 'Database update error: ' + response.status;
        console.log(errorMsg);
        const tr = document.createElement("tr");
        const td = document.createElement("td");
        td.innerHTML = errorMsg;
        tr.appendChild(td);
        resultContainer.appendChild(tr);
        return;
      }
      // response contains valid result
      response.json().then(data => {
        console.log(data);
        // update the like count in the table
        num_like.innerHTML = data.likes;
      })
    });
  }
  function add_row(data) {
  const tr = document.createElement("tr");
  tr.classList.add("mytd");
  const id = document.createElement("td");
  const name = document.createElement("td");
  const likeButtonCell = document.createElement("td");
  const numLikes = document.createElement("td");
  const uid = document.createElement("td");
  const imageCell = document.createElement("td");
  const likeButton = document.createElement("input");
  likeButton.type = "button";
  likeButton.value = "Like";
  likeButton.addEventListener("click", function() {
    like_car(data.id, data.likes, data.uid, data.name);
  });
  id.textContent = data.id;
  name.textContent = data.name;
  numLikes.textContent = data.likes ? data.likes : 0; // Check if 'likes' exists, otherwise use 0
  uid.textContent = data.uid;
  const img = document.createElement("img");
  img.src = data.image;
  img.alt = data.name;
  img.style.width = "100%";
  img.style.height = "100%";
  likeButtonCell.appendChild(likeButton);
  imageCell.appendChild(img);
  tr.appendChild(id);
  tr.appendChild(name);
  tr.appendChild(likeButtonCell);
  tr.appendChild(numLikes);
  tr.appendChild(uid);
  tr.appendChild(imageCell);
  resultContainer.appendChild(tr);
}

</script>