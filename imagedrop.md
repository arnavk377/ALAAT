<html>
<head>
    <title>Image Upload</title>
</head>
<input type="file" id="imageInput">
<button onclick="uploadImage()">Upload</button>
<img id="previewImage" src="#" alt="Preview">
<script>
function uploadImage() {
  var input = document.getElementById('imageInput');
  var preview = document.getElementById('previewImage');
  // Get the selected file
  var file = input.files[0];
  // Create a FileReader object
  var reader = new FileReader();
  // Set the image source once it's loaded
  reader.onload = function(e) {
    preview.src = e.target.result;
  };
  // Read the image file as a data URL
  reader.readAsDataURL(file);
 // Create a FormData object to store the file
      var formData = new FormData();
      formData.append('image', file);
      // Make a POST request to the server endpoint
      fetch('your_server_endpoint_url', {
        method: 'POST',
        body: formData
      })
        .then(response => {
          // Handle the response from the server
          if (response.ok) {
            alert('Image uploaded successfully!');
          } else {
            alert('Image upload failed!');
          }
        })
        .catch(error => {
          console.error('Error:', error);
        });
      // Set the image source for preview
      var reader = new FileReader();
      reader.onload = function(e) {
        preview.src = e.target.result;
      };
      reader.readAsDataURL(file);
    }
  </script>

  <style>
    #previewImage {
      width: 200px;
      height: 200px;
      margin-top: 10px;
    }
</style>
</html>




































<!--<html>
<head>
    <title>Image Upload</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            justify-content: flex-start;
            align-items: center;
            height: 100vh;
        }
        .drop-zone {
            width: 400px;
            height: 400px;
            border: 2px dashed #ccc;
            text-align: center;
            padding: 20px;
            font-size: 16px;
            margin-top: 40px;
            margin-left: auto;
            margin-right: auto;
        }
        .drop-zone.dragged-over {
            background-color: #f7f7f7;
        }
    </style>
</head>
<body>
    <div class="drop-zone" id="dropZone">
        <p>Drag and drop images here</p>
    </div>
    <script>
        const dropZone = document.getElementById('dropZone');
        dropZone.addEventListener('dragenter', (event) => {
            event.preventDefault();
            dropZone.classList.add('dragged-over');
        });
        dropZone.addEventListener('dragleave', (event) => {
            event.preventDefault();
            dropZone.classList.remove('dragged-over');
        });
        dropZone.addEventListener('dragover', (event) => {
            event.preventDefault();
        });
        dropZone.addEventListener('drop', (event) => {
            event.preventDefault();
            dropZone.classList.remove('dragged-over');
            const file = event.dataTransfer.files[0];
            const reader = new FileReader();
            reader.onload = (e) => {
                const img = new Image();
                img.src = e.target.result;
                img.onload = () => {
                    const canvas = document.createElement('canvas');
                    const ctx = canvas.getContext('2d');
                    // Set the desired width and height for the compressed image
                    const maxWidth = 800;
                    const maxHeight = 600;
                    let width = img.width;
                    let height = img.height;
                    // Calculate the new dimensions while maintaining the aspect ratio
                    if (width > maxWidth) {
                        height *= maxWidth / width;
                        width = maxWidth;
                    }
                    if (height > maxHeight) {
                        width *= maxHeight / height;
                        height = maxHeight;
                    }
                    // Set the canvas dimensions
                    canvas.width = width;
                    canvas.height = height;
                    // Draw the compressed image on the canvas
                    ctx.drawImage(img, 0, 0, width, height);
                    // Get the compressed image as a base64-encoded string
                    const compressedImage = canvas.toDataURL('image/jpeg', 0.8);
                    // Create a Blob object from the base64-encoded string
                    const byteCharacters = atob(compressedImage.split(',')[1]);
                    const byteArrays = [];
                    for (let i = 0; i < byteCharacters.length; i++) {
                        byteArrays.push(byteCharacters.charCodeAt(i));
                    }
                    const blob = new Blob([new Uint8Array(byteArrays)], { type: 'image/jpeg' });
                    // Create a FormData object to send the compressed image as multipart/form-data
                    const formData = new FormData();
                    formData.append('image', blob, 'compressed.jpg');
                    // Send the compressed image to the backend using an HTTP POST request
                    fetch('/upload', {
                        method: 'POST',
                        body: formData
                    })
                        .then(response => {
                            // Handle the response from the backend
                            console.log('Image uploaded successfully');
                        })
                            .catch(error => {
                                // Handle any errors that occurred during the upload
                                console.error('Error uploading image:', error);
                            });
                    }, 'image/jpeg', 0.8);
            };
        };
    </script>
</body>
</html>
-->