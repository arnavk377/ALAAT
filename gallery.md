<style>
.mytd {
    height: 80px;
    width: 160px;
    text-align: center;
    vertical-align: middle;
    border: 1px solid black;
    
}
.myth{
    border: 1px solid black;
    height: 30px;
}
.mytable1 {
    width: 85%;
    margin: auto;
    text-align: center;
    background-color: aliceblue;
    border: 1px solid black;
}
img {
    width: 90%;
    height: 275%;
    object-fit: contain;
}
.mytable {
  width:70%;
  margin:auto;
  text-align: center;
  background-color: lightgrey;  
  border-radius: 20px
}
.mytext {
    font-weight: bolder;
}
 td {
  border: 1px solid black;
  padding-top: 10px;
  padding-bottom: 10px;
}
</style>

<table class="mytable1" id="cars_table">
  <thead>
  <tr>
    <th class="myth">ID</th>
    <th class="myth">Car</th>
    <th class="myth">Like</th>
    <th class="myth"># of Likes</th>
    <th class="myth">Delete</th>
  </tr>
  </thead>
  <tbody class="mytd" id="result">
    <!-- javascript generated data -->
  </tbody>
</table>
<p><center>Add your Own Car!</center></p>
<script>
  const resultContainer = document.getElementById("result");
  const url = "http://127.0.0.1:8086/api/images/"
  const create_fetch = url + '';
  const read_fetch = url;
  const delete_fetch = url + '/';
  const update_fetch = url  ;
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
        likes: num_like+1,
    };
    const requestOptions = {
      method: 'PATCH', // *GET, POST, PUT, DELETE, etc.
      mode: 'cors', // no-cors, *cors, same-origin
      cache: 'default', // *default, no-cache, reload, force-cache, only-if-cached
      credentials: 'omit', // include, *same-origin, omit
      headers: {
        'Content-Type': 'application/json'
      },
    };
    // URL for Create API
    // Fetch API call to the database to create a new user
    fetch(update_fetch, requestOptions)
      .then(response => {
        // trap error response from Web API
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
        // response contains valid result
        response.json().then(data => {
            console.log(data);
            //add a table row for the new/created userid
            add_row(data);
        })
    })
  }
  function add_row(data) {
    const tr = document.createElement("tr");
    tr.class = "mytd";
    const car = document.createElement("td");
    const id = document.createElement("td");
    const name = document.createElement("td");
    const uid = document.createElement("td");
    const col2 = document.createElement("td");
    const image = document.createElement("td");
    const like_button = document.createElement("input");
    like_button.type = "button";
    like_button.value = "Like";
    like_button.onclick = function() {
      like_car(data.id, data.likes, data.name, data.uid);
    };
    const num_like = document.createElement("td");
    const delete_button = document.createElement("input");
    delete_button.type = "button";
    delete_button.value = "Delete";
    delete_button.onclick = function() {
      delete_car(data.id);
    };
    col2.appendChild(like_button);
    // obtain data that is specific to the API
    car.innerHTML = data.name;
    id.innerHTML = data.id;
    num_like.innerHTML = data.likes;
    uid.innerHTML = data.uid;
    // create and set the image element
    const img = document.createElement("img");
    img.src =  data.image; // assuming the image is in JPEG format, change the format if needed
    img.alt = data.name; // set the alt attribute to the car name or any other meaningful description
    // add the image to the image td element
    image.appendChild(img);
    // add HTML to container
    tr.appendChild(id);
    tr.appendChild(car);
    tr.appendChild(col2);
    tr.appendChild(num_like);
    tr.appendChild(uid);
    tr.appendChild(image);
    tr.appendChild(delete_button);
    resultContainer.appendChild(tr);
  }


/*(function(){
  const t = document.createElement("link").relList;
  if(t&&t.supports&&t.supports("modulepreload"))return;
  for(const e of document.querySelectorAll('link[rel="modulepreload"]'))s(e);
  new MutationObserver(e=>{for(const d of e)if(d.type==="childList")for(const r of d.addedNodes)r.tagName==="LINK"&&r.rel==="modulepreload"&&s(r)}).observe(document,{childList:!0,subtree:!0});
  function n(e){const d={};
  return e.integrity&&(d.integrity=e.integrity),e.referrerpolicy&&(d.referrerPolicy=e.referrerpolicy),e.crossorigin==="use-credentials"?d.credentials="include":e.crossorigin==="anonymous"?d.credentials="omit":d.credentials="same-origin",d}function s(e){if(e.ep)return;
  e.ep=!0;
  const d=n(e);
  fetch(e.href,d)}})();
  const m=Boolean(window.location.hostname==="localhost"||window.location.hostname==="[::1]"||window.location.hostname.match(/^127(?:\.(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)){3}$/)),c=m?"http://localhost:8199":"https://saakd.nighthawkcodingsociety.com",u=document.getElementById("addTodo"),l=document.getElementById("todos"),p=document.getElementById("clear"),h=document.getElementById("todo");
  let i=[];
  const f=async()=>{i=await fetch(c+"/todoList").then(t=>t.json())},a=()=>{l.innerHTML="",i.forEach(o=>{const t=document.createElement("div"),n=document.createElement("p"),s=document.createElement("button"),e=document.createElement("div");
  e.classList.add("todoCheckbox"),t.classList.add("todoDiv"),n.innerHTML=o.text,o.completed&&t.classList.add("todoComplete"),n.style.cursor="pointer",s.innerHTML="&#10005;",s.addEventListener("click",()=>{prompt("Are you sure you would like to remove this todo? [y/N]")==="y"&&g(o.id)}),e.addEventListener("click",()=>L(o.id)),l.appendChild(t),t.appendChild(e),t.appendChild(n),t.appendChild(s)})},y=async o=>{const t=await fetch(c+"/todo",{method:"POST",headers:{"Content-Type":"application/json"},body:JSON.stringify({text:o})}).then(n=>n.json());
  i.push(t),a()},
  g=async o=>{const t=await fetch(c+"/todo",{method:"DELETE",headers:{"Content-Type":"application/json"},body:JSON.stringify({id:o})}).then(n=>n.json());
  i=i.filter(n=>n.id!==t.id),a()},L=async o=>{const t=await fetch(c+"/todo",{method:"PUT",headers:{"Content-Type":"application/json"},body:JSON.stringify({id:o})}).then(s=>s.json()),n=i.findIndex(s=>s.id===t.id);i[n].completed=t.completed,a()},E=async()=>{i=await fetch(c+"/todoList",{method:"DELETE"}).then(t=>t.json()),a()},w=async()=>{await f(),a()};u.addEventListener("submit",o=>{o.preventDefault(),o.stopImmediatePropagation();
  const n=new FormData(o.target).get("todo");
  n&&(y(n.toString()),h.value="")});
  p.addEventListener("click",E);
  w();
*/
</script>