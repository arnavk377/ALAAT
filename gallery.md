<style>
  .table-container {
    padding-top: 20px;
    padding-bottom: 20px;
  }

  .mytd {
    text-align: center;
    vertical-align: middle;
    border: 1px solid black;
    padding: 10px;
  }

  .myth {
    border: 1px solid black;
    height: 30px;
    background-color: lightgray;
  }

  .mytable1 {
    width: 85%;
    margin: auto;
    text-align: center;
    background-color: aliceblue;
    border: 1px solid black;
    border-collapse: collapse;
  }

  .mytable1 th,
  .mytable1 td {
    padding: 10px;
    border: 1px solid black;
  }

  img {
    display: block;
    width: 100%;
    height: auto;
    object-fit: cover;
    border-radius: 8px;
  }

  .like-button {
    padding: 8px 12px;
    background-color: #4caf50;
    color: #ffffff;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }

  .like-button:hover {
    background-color: #45a049;
  }
</style>

<div class="table-container">
  <table class="mytable1" id="cars_table">
    <thead>
      <tr>
        <th class="myth">ID</th>
        <th class="myth">Image Name</th>
        <th class="myth">Like</th>
        <th class="myth"># of Likes</th>
        <th class="myth">Image</th>
      </tr>
    </thead>
    <tbody class="mytd" id="result">
      <!-- JavaScript generated data -->
    </tbody>
  </table>
</div>

<script>
  const resultContainer = document.getElementById("result");
  const url = "http://127.0.0.1:8086/api/images/";
  const read_fetch = url;
  const update_fetch = url;

  // Load images on page entry
  read_images();

  // Display image table; data is fetched from the backend API
  function read_images() {
    const read_options = {
      method: "GET",
      mode: "cors",
      cache: "default",
      credentials: "omit",
      headers: {
        "Content-Type": "application/json",
      },
    };

    fetch(read_fetch, read_options)
      .then((response) => {
        if (response.status !== 200) {
          const errorMsg = "Database read error: " + response.status;
          console.log(errorMsg);
          const tr = document.createElement("tr");
          const td = document.createElement("td");
          td.innerHTML = errorMsg;
          tr.appendChild(td);
          resultContainer.appendChild(tr);
          return;
        }

        response.json().then((data) => {
          console.log(data);
          for (let row of data) {
            console.log(row);
            add_row(row);
          }
        });
      })
      .catch((err) => {
        console.error(err);
        const tr = document.createElement("tr");
        const td = document.createElement("td");
        td.innerHTML = err;
        tr.appendChild(td);
        resultContainer.appendChild(tr);
      });
  }

  function like_image(image_id, num_likes, image_uid, image_name, likeButton) {
    const body = {
      id: image_id,
      uid: image_uid,
      name: image_name,
      likes: num_likes + 1,
    };

    const requestOptions = {
      method: "PATCH",
      mode: "cors",
      cache: "default",
      credentials: "omit",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(body),
    };

    fetch(update_fetch, requestOptions)
      .then((response) => {
        if (response.status !== 200) {
          const errorMsg = "Database update error: " + response.status;
          console.log(errorMsg);
          const tr = document.createElement("tr");
          const td = document.createElement("td");
          td.innerHTML = errorMsg;
          tr.appendChild(td);
          resultContainer.appendChild(tr);
          return;
        }

        response.json().then((data) => {
          console.log(data);
          // Update the like count in the table
          num_likes.textContent = data.likes;
        });
      })
      .catch((err) => {
        console.error(err);
        const tr = document.createElement("tr");
        const td = document.createElement("td");
        td.innerHTML = err;
        tr.appendChild(td);
        resultContainer.appendChild(tr);
      });
  }

  function add_row(data) {
    const tr = document.createElement("tr");
    tr.classList.add("mytd");

    const id = document.createElement("td");
    const name = document.createElement("td");
    const likeButtonCell = document.createElement("td");
    const numLikes = document.createElement("td");
    const imageCell = document.createElement("td");
    const likeButton = document.createElement("button"); // Change input type to 'button'

    likeButton.textContent = "Like";
    likeButton.addEventListener("click", function () {
      like_image(data.id, data.likes, data.uid, data.name, likeButton);
    });

    id.textContent = data.id;
    name.textContent = data.name;
    numLikes.textContent = data.likes ? data.likes : 0;

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
    tr.appendChild(imageCell);

    resultContainer.appendChild(tr);
  }
</script>
