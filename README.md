<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Álbum Endoscopia Nicaragua ROALPI</title>
    <style>
        body {
            margin: 0;
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            color: #333;
        }
        header {
            background-color: #006699;
            color: white;
            padding: 20px;
            text-align: center;
        }
        .container {
            padding: 20px;
            max-width: 1200px;
            margin: auto;
        }
        .search-bar {
            margin-bottom: 20px;
            text-align: center;
        }
        .search-bar input,
        .search-bar select,
        .search-bar button {
            width: 40%;
            padding: 10px;
            font-size: 16px;
            border: 1px solid #ccc;
            border-radius: 5px;
            margin: 5px;
        }
        .video-gallery {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 20px;
        }
        .video-card {
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
            overflow: hidden;
            text-align: center;
        }
        .video-card iframe {
            width: 100%;
            height: 200px;
        }
        .video-card p {
            padding: 10px;
            margin: 0;
            font-weight: bold;
        }
        .video-card a.download-link {
            display: inline-block;
            margin: 10px;
            padding: 8px 12px;
            background-color: #006699;
            color: white;
            text-decoration: none;
            border-radius: 5px;
            font-size: 14px;
        }
        .video-card a.download-link:hover {
            background-color: #004466;
        }
        footer {
            background-color: #004466;
            color: white;
            text-align: center;
            padding: 15px;
            margin-top: 40px;
        }
        .upload-section {
            text-align: center;
            margin: 20px 0;
        }
        .upload-section input,
        .upload-section select,
        .upload-section button {
            margin: 5px;
            padding: 10px;
            font-size: 16px;
            border: 1px solid #ccc;
            border-radius: 5px;
        }
    </style>
</head>
<body>
    <header>
        <h1>Álbum Endoscopia Nicaragua ROALPI</h1>
        <p>Catálogo educativo de procedimientos endoscópicos del Centro Nacional de Endoscopía Hospital Alemán Nicaragüense</p>
    </header>

    <div class="container">
        <div class="search-bar">
            <input type="text" id="searchInput" placeholder="Buscar videos..." onkeyup="filterVideos()" />
            <select id="categoryFilter" onchange="filterVideos()">
                <option value="">Todas las categorías</option>
                <option value="Colonoscopia">Colonoscopia</option>
                <option value="Gastroscopia">Gastroscopia</option>
            </select>
        </div>

        <div class="upload-section">
            <h3>Agregar nuevo video (solo enlaces)</h3>
            <input type="text" id="newVideoTitle" placeholder="Título del video" />
            <select id="newVideoCategory">
                <option value="Colonoscopia">Colonoscopia</option>
                <option value="Gastroscopia">Gastroscopia</option>
            </select>
            <input type="text" id="newVideoURL" placeholder="URL de YouTube (ej: https://www.youtube.com/watch?v=abc123)" />
            <button onclick="addVideo()">Agregar Video</button>
        </div>

        <div class="video-gallery" id="videoGallery">
            <!-- Videos cargados desde YouTube -->
            <div class="video-card" data-title="Video de ejemplo 1" data-category="Colonoscopia">
                <iframe src="https://www.youtube.com/embed/hEHM_PFZZo0" frameborder="0" allowfullscreen></iframe>
                <p>Video de ejemplo 1</p>
                <a class="download-link" href="https://www.ssyoutube.com/watch?v=hEHM_PFZZo0" target="_blank">📥 Descargar video</a>
            </div>
            <div class="video-card" data-title="Video de ejemplo 2" data-category="Gastroscopia">
                <iframe src="https://www.youtube.com/embed/XEepqhqNZtQ" frameborder="0" allowfullscreen></iframe>
                <p>Video de ejemplo 2</p>
                <a class="download-link" href="https://www.ssyoutube.com/watch?v=XEepqhqNZtQ" target="_blank">📥 Descargar video</a>
            </div>
        </div>
    </div>

    <footer>
        <p>&copy; 2025 Dr(a). Nombre Apellido | Todos los derechos reservados</p>
    </footer>

    <script>
        function filterVideos() {
            const input = document.getElementById('searchInput').value.toLowerCase();
            const category = document.getElementById('categoryFilter').value;
            const cards = document.getElementsByClassName('video-card');
            Array.from(cards).forEach(card => {
                const title = card.getAttribute('data-title').toLowerCase();
                const cardCategory = card.getAttribute('data-category');
                card.style.display = (title.includes(input) && (!category || cardCategory === category)) ? '' : 'none';
            });
        }
        function addVideo() {
            const title = document.getElementById('newVideoTitle').value;
            const category = document.getElementById('newVideoCategory').value;
            const url = document.getElementById('newVideoURL').value;
            let videoId = '';
            if (url.includes('youtube.com/watch?v=')) videoId = url.split('v=')[1].split('&')[0];
            else if (url.includes('youtu.be/')) videoId = url.split('youtu.be/')[1];
            else { alert('URL de YouTube no válida'); return; }
            if (title && category && videoId) {
                const gallery = document.getElementById('videoGallery');
                const newCard = document.createElement('div');
                newCard.className = 'video-card';
                newCard.setAttribute('data-title', title);
                newCard.setAttribute('data-category', category);
                newCard.innerHTML = `
                    <iframe src="https://www.youtube.com/embed/${videoId}" frameborder="0" allowfullscreen></iframe>
                    <p>${title}</p>
                    <a class="download-link" href="https://www.ssyoutube.com/watch?v=${videoId}" target="_blank">📥 Descargar video</a>
                `;
                gallery.appendChild(newCard);
                document.getElementById('newVideoTitle').value = '';
                document.getElementById('newVideoURL').value = '';
            } else alert('Por favor completa todos los campos correctamente.');
        }
    </script>
</body>
</html>
