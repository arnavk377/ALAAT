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
        #imagePreview {
            width: 200px;
            height: auto;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <form id="uploadForm">
        <div class="drop-zone" id="dropZone">
            <p>Drag and drop images here</p>
        </div>
        <div>
            <label for="imageName">Image Name:</label>
            <input type="text" id="imageName" name="name">
        </div>
        <div>
            <label for="uid">UID:</label>
            <input type="text" id="uid" name="uid">
        </div>
        <input type="submit" value="Upload">
    </form>
    <img id="imagePreview" src="#" alt="Preview" style="display: none;">
    <script>
      const dropZone = document.getElementById('dropZone');
      const imagePreview = document.getElementById('imagePreview');
      const uploadForm = document.getElementById('uploadForm');
      let base64Image = ''; // Variable to store the base64 value of the image
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
          dropZone.classList.add('dragged-over');
      });
      dropZone.addEventListener('drop', (event) => {
          event.preventDefault();
          dropZone.classList.remove('dragged-over');
          const file = event.dataTransfer.files[0];
          const reader = new FileReader();
          reader.onload = (e) => {
              imagePreview.src = e.target.result;
              imagePreview.style.display = 'block';
              base64Image = e.target.result.split(',')[1]; // Extract base64 value
          };
          reader.readAsDataURL(file);
      });
      uploadForm.addEventListener('submit', (event) => {
          event.preventDefault();
          const formData = {
              image: base64Image,
              name: uploadForm.elements.imageName.value,
              uid: uploadForm.elements.uid.value,
              likes: '0'
          };
          const requestOptions = {
              method: 'POST',
              body: JSON.stringify(formData),
              mode: 'cors', // headers for cors policy
              cache: 'default', // cache header
              credentials: 'omit', // header for credentials
              headers: {
                  'Content-Type': 'application/json',
                  'Authorization': 'Bearer my-token',
              },
          };
          fetch('https://alaat.duckdns.org/api/images/', requestOptions)
              .then(response => {
                  console.log('Image uploaded successfully');
                  // Reset form and image preview
                  uploadForm.reset();
                  imagePreview.src = '#';
                  imagePreview.style.display = 'none';
                  base64Image = ''; // Clear base64Image for the next upload
              })
              .catch(error => {
                  console.error('Error uploading image:', error);
              });
      });
</script>

</body>
</html>
