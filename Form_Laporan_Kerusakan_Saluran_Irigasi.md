<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Ambil Lokasi Otomatis</title>
    <style>
      body {
        font-family: Arial, sans-serif;
        padding: 2rem;
        text-align: center;
      }

      #btn {
        display: none;
        background-color: #4CAF50;
        color: white;
        text-decoration: none;
        padding: 12px 24px;
        font-size: 1rem;
        border-radius: 6px;
        margin-top: 20px;
        display: inline-block;
      }

      #btn:hover {
        background-color: #45a049;
      }

      .loading {
        font-size: 1.1rem;
        color: #333;
      }
    </style>
  </head>
  <body>
    <h2>📍 Mengambil lokasi Anda...</h2>
    <p id="lokasi" class="loading">Mohon tunggu sebentar. Jika muncul permintaan izin lokasi, klik "Izinkan".</p>

    <!-- Tombol redirect sebagai LINK (bukan JavaScript redirect) -->
    <a id="btn" href="#" target="_blank">👉 Buka Formulir dengan Lokasi</a>

    <script>
      const formUrl = "https://docs.google.com/forms/d/e/1FAIpQLSeOzz2go9aH1gTBoCMjdvd2DaVyzyS2jMqXeiQz1uvnG0eHSg/viewform";
      const entryKey = "entry.1348648326"; // Entry untuk koordinat (ganti sesuai form Anda)

      const lokasiText = document.getElementById("lokasi");
      const btn = document.getElementById("btn");

      function tampilkanForm(lat, lng) {
        const koordinat = `${lat},${lng}`;
        const finalUrl = `${formUrl}?${entryKey}=${encodeURIComponent(koordinat)}`;

        lokasiText.innerText = `Lokasi berhasil didapat: ${koordinat}`;
        btn.href = finalUrl;
        btn.style.display = "inline-block";

        console.log("🔁 Redirect ke Form:", finalUrl);
      }

      function gagal(msg) {
        lokasiText.innerText = "⚠️ Gagal mengambil lokasi: " + msg;
      }

      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(
          pos => tampilkanForm(pos.coords.latitude, pos.coords.longitude),
          err => gagal(err.message),
          { enableHighAccuracy: true, timeout: 10000 }
        );
      } else {
        gagal("Browser tidak mendukung geolokasi.");
      }
    </script>
  </body>
</html>
