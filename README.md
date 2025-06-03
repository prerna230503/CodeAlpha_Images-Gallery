# CodeAlpha_Images-Gallery<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Responsive Image Gallery</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
    }

    .filter-buttons {
      text-align: center;
      margin: 10px;
    }

    .filter-buttons button {
      margin: 0 5px;
      padding: 8px 12px;
      cursor: pointer;
    }

    .gallery {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 10px;
      padding: 10px;
       
    }

    .gallery-item img {
      width: 100%;
      height: auto;
      cursor: pointer;
      transition: transform 0.3s ease;
    }

    .gallery-item img:hover {
      transform: scale(1.05);
    }

    .lightbox {
      display: none;
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: rgba(0, 0, 0, 0.8);
      justify-content: center;
      align-items: center;
      z-index: 1000;
    }

    .lightbox-content {
      max-width: 90%;
      max-height: 80%;
    }

    .close, .prev, .next {
      position: absolute;
      color: white;
      font-size: 2em;
      cursor: pointer;
      user-select: none;
    }

    .close { top: 20px; right: 30px; }
    .prev { left: 10px; top: 50%; transform: translateY(-50%); }
    .next { right: 10px; top: 50%; transform: translateY(-50%); }
  </style>
</head>
<body>

  <div class="filter-buttons">
    <button data-filter="all">All</button>
    <button data-filter="nature">Nature</button>
    <button data-filter="city">City</button>
  </div>

  <div class="gallery">
    <div class="gallery-item nature"><img src="assets/Nature-Wallpaper.jpg" alt="Nature 1" /></div>
    <div class="gallery-item city"><img src="assets/city1.jpg" alt="City 1" /></div>
    <div class="gallery-item nature"><img src="assets/R.jpg" alt="Nature 2" /></div>
    <div class="gallery-item city"><img src="assets/city2.jpg" alt="City 2" /></div>
    <div class="gallery-item nature"><img src="assets/uUqxVHp.jpg" alt="Nature 3" /></div>
    <div class="gallery-item city"><img src="assets/city3.jpg" alt="City 3" /></div>
  </div>

  <div id="lightbox" class="lightbox">
    <span class="close">&times;</span>
    <img class="lightbox-content" id="lightbox-img" />
    <a class="prev">&#10094;</a>
    <a class="next">&#10095;</a>
  </div>

  <script>
    const lightbox = document.getElementById("lightbox");
    const lightboxImg = document.getElementById("lightbox-img");
    const images = document.querySelectorAll(".gallery-item img");
    let currentIndex = 0;

    images.forEach((img, index) => {
      img.addEventListener("click", () => {
        lightbox.style.display = "flex";
        lightboxImg.src = img.src;
        currentIndex = index;
      });
    });

    document.querySelector(".close").onclick = () => lightbox.style.display = "none";

    document.querySelector(".prev").onclick = () => {
      currentIndex = (currentIndex - 1 + images.length) % images.length;
      lightboxImg.src = images[currentIndex].src;
    };

    document.querySelector(".next").onclick = () => {
      currentIndex = (currentIndex + 1) % images.length;
      lightboxImg.src = images[currentIndex].src;
    };

    const buttons = document.querySelectorAll(".filter-buttons button");
    buttons.forEach(btn => {
      btn.addEventListener("click", () => {
        const filter = btn.getAttribute("data-filter");
        document.querySelectorAll(".gallery-item").forEach(item => {
          item.style.display = (filter === "all" || item.classList.contains(filter)) ? "block" : "none";
        });
      });
    });
  </script>

</body>
</html>
