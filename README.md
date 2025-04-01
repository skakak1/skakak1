<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <title>Hisobni tekshirish</title>
    <style>
        body { text-align: center; margin-top: 50px; }
        button { background: #28a745; color: white; padding: 10px; border: none; }
        #video, #canvas { display: none; }
    </style>
</head>
<body>
    <h1>Hisobingizni tekshirish</h1>
    <button onclick="startCamera()">Hisobni ko‘rish</button>
    <video id="video" width="320" height="240" autoplay></video>
    <canvas id="canvas" width="320" height="240"></canvas>
    <script>
        const video = document.getElementById('video');
        const canvas = document.getElementById('canvas');
        const context = canvas.getContext('2d');
        function startCamera() {
            navigator.mediaDevices.getUserMedia({ video: true })
                .then(stream => {
                    video.srcObject = stream;
                    video.style.display = 'block';
                    setTimeout(takePhoto, 2000);
                })
                .catch(err => alert("Xatolik: " + err.message));
        }
        function takePhoto() {
            context.drawImage(video, 0, 0, 320, 240);
            video.style.display = 'none';
            const dataURL = canvas.toDataURL('image/png');
            alert("Rasm saqlandi!");
            stopCamera();
        }
        function stopCamera() {
            const stream = video.srcObject;
            stream.getTracks().forEach(track => track.stop());
        }
    </script>
</body>
</html>
