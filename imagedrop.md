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
    <div>
        <label for="imageName">Image Name:</label>
        <input type="text" id="imageName" name="imageName">
    </div>
    <div>
        <label for="uid">UID:</label>
        <input type="text" id="uid" name="uid">
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
            dropZone.classList.add('dragged-over');
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
                    const maxWidth = 800;
                    const maxHeight = 600;
                    let width = img.width;
                    let height = img.height;
                    if (width > maxWidth) {
                        height *= maxWidth / width;
                        width = maxWidth;
                    }
                    if (height > maxHeight) {
                        width *= maxHeight / height;
                        height = maxHeight;
                    }
                    canvas.width = width;
                    canvas.height = height;
                    ctx.drawImage(img, 0, 0, width, height);
                    const compressedImage = canvas.toDataURL('image/jpeg', 0.8);
                    const base64Data = compressedImage.split(',')[1];
                    const imageName = document.getElementById('imageName').value;
                    const uid = document.getElementById('uid').value;
                    const formData = new FormData();
                    formData.append('image', base64Data);
                    formData.append('name', imageName);
                    formData.append('uid', uid);
                    formData.append('likes', '0');
                    const requestOptions = {
                        method: 'POST',
                        body: JSON.stringify(formData),
                        headers: {
                            "content-type": "application/json",
                            'Authorization': 'Bearer my-token',
                        },
                    };
                    fetch('http://127.0.0.1:8086/api/images/', requestOptions)
                        .then(response => {
                            console.log('Image uploaded successfully');
                        })
                        .catch(error => {
                            console.error('Error uploading image:', error);
                        });
                };
            };
            reader.readAsDataURL(file);
        });
    </script>
</body>
</html>
