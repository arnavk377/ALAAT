<html>
<head>
    <title>Image Upload</title>
    <style>
        .drop-zone {
            margin-top: 20px;
            margin-left: auto;
            margin-right: auto;
            display: flex;
            justify-content: center;
            align-items: center;
            width: 400px;
            height: 400px;
            border: 2px dashed #ccc;
            text-align: center;
            padding: 20px;
            font-size: 16px;
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
        // Handle the dragover event
        dropZone.addEventListener('dragover', (e) => {
            e.preventDefault();
            dropZone.classList.add('dragged-over');
        });
        // Handle the dragleave event
        dropZone.addEventListener('dragleave', () => {
            dropZone.classList.remove('dragged-over');
        });
        // Handle the drop event
        dropZone.addEventListener('drop', (e) => {
            e.preventDefault();
            dropZone.classList.remove('dragged-over');
            handleDrop(e.dataTransfer.files);
        });
        // Function to handle the dropped files
        function handleDrop(files) {
            for (let i = 0; i < files.length; i++) {
                const file = files[i];
                const formData = new FormData();
                formData.append('image', file);
                // Send the image file to the backend
                uploadImage(formData);
            }
        }
        // Function to upload the image to the backend
        function uploadImage(formData) {
            fetch('/upload', {
                method: 'POST',
                body: formData
            })
            .then(response => response.json())
            .then(data => {
                console.log('Image uploaded successfully:', data);
                // Handle the response from the backend, if needed
            })
            .catch(error => {
                console.error('Error uploading image:', error);
                // Handle the error, if needed
            });
        }
    </script>
</body>
</html>