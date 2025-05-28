<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8" />
  <title>9Anime Uploader</title>
  <script src="https://telegram.org/js/telegram-web-app.js"></script>
  <style>
    body { font-family: sans-serif; padding: 20px; text-align: center; }
    button { padding: 10px 20px; font-size: 16px; margin-top: 10px; }
  </style>
</head>
<body>
  <h2>📺 Upload Your Anime Clip</h2>
  <input id="videoInput" type="file" accept="video/*" />
  <br />
  <button onclick="uploadVideo()">🚀 Upload</button>

  <script>
    const tg = window.Telegram.WebApp;
    tg.expand();

    async function uploadVideo() {
      const input = document.getElementById("videoInput");
      const file = input.files[0];
      if (!file) return alert("Please select a video!");

      if (file.size > 100 * 1024 * 1024) {
        return alert("⚠️ File must be under 100MB");
      }

      const formData = new FormData();
      formData.append("video", file);
      formData.append("user_id", tg.initDataUnsafe?.user?.id || "unknown");

      const res = await fetch("https://your-backend.com/upload", {
        method: "POST",
        body: formData,
      });

      const result = await res.json();
      alert(result.message || "Uploaded!");
    }
  </script>
</body>
</html>

