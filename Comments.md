<html>
  <head>
    <title>User Comments</title>
    <style>
      .container {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin-top: 50px;
      }

      .Commentssection {
        width: 80%;
        text-align: center;
      }

      #comments {
        background-color: lightgray;
        padding: 10px;
        border-radius: 10px;
        margin-bottom: 20px;
      }

      #delete-all-comments-button {
        margin-bottom: 20px;
        padding: 10px 20px;
        background-color: lightblue;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
      }

      #comment-form {
        width: 60%;
        background-color: lightgray;
        padding: 20px;
        border-radius: 10px;
      }

      #comment-form label {
        display: block;
        margin-bottom: 10px;
      }

      input[type="text"],
      textarea {
        width: 100%;
        padding: 10px;
        border-radius: 5px;
        border: 1px solid gray;
      }

      button[type="submit"] {
        padding: 10px 20px;
        background-color: lightblue;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
      }

      p {
        margin: 10px;
      }
    </style>
  </head>
  <body>
    
    <div class="container">
      <div class="Commentssection">
        <h1>User Comments</h1>
        <div id="comments">
          <!-- comments will be displayed here -->
        </div>
        <button id="delete-all-comments-button">Delete All Comments</button>
      </div>
      <h2>Add a Comment</h2>
      <form id="comment-form">
        <label>
          Name:
          <input type="text" id="username" required>
        </label>
        <br><br>
        <label>
          Comment:
          <textarea id="comment" required></textarea>
        </label>
        <br><br>
        <button type="submit">Submit</button>
      </form>
    </div>

    <script>
      const commentsDiv = document.querySelector('#comments');
      const deleteAllCommentsButton = document.querySelector('#delete-all-comments-button');

      // Fetch comments and display them
      async function fetchAndDisplayComments() {
        try {
          const response = await fetch('http://127.0.0.1:8086/comments');
          const comments = await response.json();
          commentsDiv.innerHTML = '';
          comments.forEach(comment => {
            commentsDiv.innerHTML += `
              <p><strong>${comment[1]}</strong> said: ${comment[2]}</p>
            `;
          });
        } catch (error) {
          console.error(error);
        }
      }

      // Delete all comments
      async function deleteAllComments() {
        try {
          const response = await fetch('http://127.0.0.1:8086/comments', {
            method: 'DELETE',
          });
          if (response.ok) {
            commentsDiv.innerHTML = '';
          }
        } catch (error) {
          console.error(error);
        }
      }

      // Handle button click events
      deleteAllCommentsButton.addEventListener('click', async event => {
        event.preventDefault();
        await deleteAllComments();
      });

      const form = document.querySelector('form');

      // Handle form submissions
      form.addEventListener('submit', async event => {
        event.preventDefault();
        const username = document.querySelector('#username').value;
        const comment = document.querySelector('#comment').value;
        const response = await fetch('http://127.0.0.1:8086/comments', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          mode: 'cors',
          credentials: 'omit',
          body: JSON.stringify({ username, comment }),
        });
        if (response.ok) {
          form.reset();
          fetchAndDisplayComments();
        }
      });

      fetchAndDisplayComments();
    </script>
  </body>
</html>
