<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Galeri OSIS Kesenian</title>
  <style>
    @keyframes fadeIn {
      from { opacity: 0; transform: scale(0.95); }
      to { opacity: 1; transform: scale(1); }
    }

    .start-box {
      animation: fadeIn 1s ease-out;
    }
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background: #f8f8ff;
      overflow-x: hidden;
    }

    .start-page {
      position: fixed;
      inset: 0;
      background-color: rgba(255, 240, 245, 0.95);
      display: flex;
      justify-content: center;
      align-items: center;
      flex-direction: column;
      z-index: 9999;
      transition: opacity 0.6s ease;
    }

    .start-page.hidden {
      display: none;
    }

    .start-box {
      background: #fff;
      border-radius: 20px;
      padding: 30px;
      max-width: 90%;
      text-align: center;
      box-shadow: 0 8px 20px rgba(0,0,0,0.2);
    }

    .start-box h2 {
      font-size: 18px;
      color: #d36c6c;
      margin-bottom: 20px;
    }

    .choice-button {
      background-color: #ffb6c1;
      border: none;
      border-radius: 12px;
      padding: 10px 20px;
      margin: 10px;
      color: white;
      font-weight: bold;
      cursor: pointer;
      transition: background-color 0.3s;
    }

    .choice-button:hover {
      background-color: #e69aa9;
    }

    header {
      text-align: center;
      padding: 20px;
      background-color: #fff0f5;
      color: #a0522d;
      font-size: 24px;
      font-weight: bold;
      box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    }

    .book {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
      gap: 20px;
      padding: 30px;
      max-width: 1200px;
      margin: auto;
    }

    .page {
      transform-style: preserve-3d;
      transition: transform 0.6s ease;
    }

    .page:hover {
      transform: rotateY(-5deg) scale(1.03);
    }

    .photo-card {
      position: relative;
      width: 100%;
      border-radius: 16px;
      overflow: hidden;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
      background-color: #fff;
      transition: transform 0.3s;
    }

    .photo-card img {
      width: 100%;
      height: auto;
      display: block;
    }

    .upload-box-inline {
      text-align: center;
      margin-top: 10px;
    }

    .upload-box-inline input[type="file"] {
      margin: 5px;
    }

    .prayer-box {
      padding: 10px;
      background-color: #fffafc;
      border-top: 1px solid #eee;
    }

    .prayer-box textarea {
      width: 100%;
      height: 80px;
      resize: none;
      padding: 8px;
      border-radius: 8px;
      border: 1px solid #ccc;
      font-family: inherit;
    }

    .prayer-box button {
      margin-top: 8px;
      padding: 6px 12px;
      border: none;
      border-radius: 8px;
      background-color: #ffb6c1;
      color: white;
      cursor: pointer;
    }

    .upload-background, .music-upload {
      text-align: center;
      padding: 20px;
    }

    audio {
      position: fixed;
      bottom: 20px;
      left: 50%;
      transform: translateX(-50%);
      z-index: 999;
    }
  </style>
</head>
<body>
  <div class="start-page" id="startPage">
    <div class="start-box">
  <h2>Seberapa kesenian kah kamu?</h2>
  <p style="margin-bottom:20px; color:#555">Untuk anak-anak dari division of the year yaitu KESENIAN yang isinya manusia bernada banget pokoknya</p>
  <button class="choice-button" onclick="hideStart()">kesenian banget</button>
  <button class="choice-button" onclick="hideStart()">CHUSSS NDA USAH DIRAGUKAN LAGI JIWA SENI KU</button>
</div>
  </div>

  <header>🖼️ Our Core Memories 🤍🎼
  <div style="font-size: 14px; color: #8b5e3c; margin-top: 4px;">kesenian 24/25</div>
</header>

  <div class="upload-background">
    <label for="bgInput">Pilih Background:</label>
    <input type="file" id="bgInput" accept="image/*" />
  </div>

  <div class="music-upload">
    <label for="musicInput">Pilih Musik:</label>
    <input type="file" id="musicInput" accept="audio/*" />
  </div>

  <div class="book" id="bookGallery"></div>

  <audio id="audioPlayer" controls autoplay loop>
    <source src="" type="audio/mpeg">
    Browsermu tidak mendukung audio.
  </audio>

  <script>
    function hideStart() {
      const startPage = document.getElementById('startPage');
      startPage.style.transition = 'opacity 0.6s ease';
      startPage.style.opacity = '0';
      setTimeout(() => startPage.classList.add('hidden'), 600);
      document.getElementById('startPage').classList.add('hidden');
    }

    document.getElementById('bgInput').addEventListener('change', function(event) {
      const file = event.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = function(e) {
          document.body.style.backgroundImage = `url('${e.target.result}')`;
        };
        reader.readAsDataURL(file);
      }
    });

    document.getElementById('musicInput').addEventListener('change', function(event) {
      const file = event.target.files[0];
      if (file) {
        const reader = new FileReader();
        reader.onload = function(e) {
          const audio = document.getElementById('audioPlayer');
          audio.src = e.target.result;
          audio.play();
        };
        reader.readAsDataURL(file);
      }
    });

    const bookGallery = document.getElementById('bookGallery');

    for (let i = 1; i <= 15; i++) {
      const page = document.createElement('div');
      page.className = 'page';
      const placeholder = `https://via.placeholder.com/300x200?text=Foto+${i}`;
      page.innerHTML = `
        <div class="photo-card">
          <img src="${placeholder}" alt="Foto ${i}" />
          <div class="upload-box-inline">
            <input type="file" accept="image/*" />
          </div>
          <div class="prayer-box">
            <textarea placeholder="Doa, pesan atau kalimat berkesan kamu..."></textarea>
            <button>Simpan</button>
          </div>
        </div>
      `;
      bookGallery.appendChild(page);
    }

    const fileInputs = document.querySelectorAll('.upload-box-inline input[type="file"]');
    const imageTags = document.querySelectorAll('.photo-card img');

    fileInputs.forEach((input, index) => {
      input.addEventListener('change', function(event) {
        const file = event.target.files[0];
        if (file) {
          const reader = new FileReader();
          reader.onload = function(e) {
            imageTags[index].src = e.target.result;
          };
          reader.readAsDataURL(file);
        }
      });
    });
  </script>
</body>
</html>
