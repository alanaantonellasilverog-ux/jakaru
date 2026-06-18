<!DOCTYPE html>
<html lang="gn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Ka Karu - ¡A comer!</title>
    <style>
        :root {
            --vivid-orange: #FF6B00; /* Un naranja muy vivo y llamativo */
            --light-orange: #FFE5D0;
            --dark-teal: #004D4D; /* Color oscuro para contraste */
            --white: #FFFFFF;
            --grey: #A0A0A0;
            --badge-green: #2ecc71; /* Verde vivo para la promo */
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Poppins', 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; /* Tipografía más moderna y viva */
        }

        body {
            background-color: var(--light-orange); /* Fondo suave en tono naranja */
            color: var(--dark-teal);
            padding-bottom: 20px;
        }

        /* Header */
        header {
            background-color: var(--vivid-orange); /* Fondo naranja vivo */
            padding: 30px 20px;
            text-align: center;
            box-shadow: 0 4px 10px rgba(0,0,0,0.15);
            position: sticky;
            top: 0;
            z-index: 100;
            border-bottom-left-radius: 20px;
            border-bottom-right-radius: 20px;
        }

        header h1 {
            color: var(--white); /* Texto en blanco */
            font-size: 32px;
            font-weight: 900;
            margin-bottom: 8px;
            letter-spacing: -1px;
        }

        header p {
            font-size: 16px;
            color: var(--white);
            opacity: 0.9;
        }

        /* Buscador y Filtros */
        .search-container {
            padding: 20px;
        }

        .search-bar {
            width: 100%;
            padding: 15px 25px;
            border: 2px solid var(--vivid-orange); /* Borde naranja vivo */
            border-radius: 30px;
            font-size: 16px;
            outline: none;
            box-shadow: 0 4px 8px rgba(0,0,0,0.05);
            background-color: var(--white);
        }

        .filters {
            display: flex;
            gap: 12px;
            overflow-x: auto;
            padding: 5px 20px 20px 20px;
            scrollbar-width: none;
        }

        .filters::-webkit-scrollbar {
            display: none;
        }

        .filter-btn {
            background-color: var(--white);
            color: var(--vivid-orange);
            padding: 10px 20px;
            border-radius: 25px;
            border: 2px solid var(--vivid-orange);
            font-size: 14px;
            font-weight: 700;
            white-space: nowrap;
            cursor: pointer;
            transition: all 0.3s;
        }

        .filter-btn.active, .filter-btn:hover {
            background-color: var(--vivid-orange);
            color: var(--white);
            border-color: var(--vivid-orange);
        }

        /* Lista de Locales */
        .feed {
            padding: 0 20px;
            display: flex;
            flex-direction: column;
            gap: 25px;
        }

        .card {
            background-color: var(--white);
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 6px 18px rgba(0,0,0,0.08);
            transition: transform 0.3s;
        }

        .card:hover {
            transform: translateY(-5px); /* Pequeño efecto al pasar el mouse */
        }

        .card-img {
            width: 100%;
            height: 200px;
            background-size: cover;
            background-position: center;
            position: relative;
        }

        .promo-badge {
            position: absolute;
            top: 20px;
            left: 20px;
            background-color: var(--badge-green); /* Verde vivo para la promo */
            color: var(--white);
            padding: 8px 16px;
            border-radius: 25px;
            font-size: 13px;
            font-weight: bold;
            box-shadow: 0 3px 8px rgba(0,0,0,0.2);
            text-transform: uppercase;
        }

        .card-content {
            padding: 20px;
        }

        .card-title {
            font-size: 22px;
            font-weight: 800;
            margin-bottom: 8px;
            color: var(--dark-teal);
        }

        .card-tag {
            font-size: 13px;
            color: var(--vivid-orange);
            font-weight: 700;
            text-transform: uppercase;
            margin-bottom: 10px;
        }

        .card-info {
            font-size: 15px;
            color: var(--grey);
            margin-bottom: 18px;
        }

        .card-btn {
            display: block;
            width: 100%;
            text-align: center;
            background-color: var(--dark-teal); /* Color de contraste para el botón */
            color: var(--white);
            padding: 14px;
            border-radius: 12px;
            text-decoration: none;
            font-size: 15px;
            font-weight: 700;
            transition: background 0.3s;
        }

        .card-btn:hover {
            background-color: #003333;
        }
    </style>
    <!-- Importar tipografía moderna Poppins -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@600;700;800;900&display=swap" rel="stylesheet">
</head>
<body>

    <header>
        <h1>Ka Karu</h1>
        <p>¡A comer! - Jajapóke pe karu</p>
    </header>

    <div class="search-container">
        <input type="text" id="searchInput" class="search-bar" placeholder="¿Mbae rejapóta karu ko'ápe? (¿Qué quieres comer?)">
    </div>

    <div class="filters">
        <button class="filter-btn active" onclick="filterCategory('todos')">Opavave (Todos)</button>
        <button class="filter-btn" onclick="filterCategory('burgers')">Burgers</button>
        <button class="filter-btn" onclick="filterCategory('bar')">Bar & Pub</button>
        <button class="filter-btn" onclick="filterCategory('pizza')">Pizza</button>
        <button class="filter-btn" onclick="filterCategory('cafe')">Café</button>
    </div>

    <div class="feed" id="localesFeed">
        <!-- Los locales se cargan dinámicamente con JavaScript -->
    </div>

    <script>
        // Base de datos simulada de los locales (Puedes personalizarla aquí)
        const locales = [
            {
                nombre: "Hamburpete - Villa Morra",
                categoria: "burgers",
                tag: "Hamburguesas con Sabor",
                promo: "Promosión: 2x1 Burgers ko'árõ (Martes)",
                direccion: "Mcal. López e/ Cruz del Chaco",
                imagen: "https://images.unsplash.com/photo-1568901346375-23c9450c58cd?q=80&w=500",
                linkMapa: "https://waze.com/ul?q=Villa%20Morra,%20Asunción"
            },
            {
                nombre: "El Tereré Bar - Oguapyhápe",
                categoria: "bar",
                tag: "Bar & Restó de Amigos",
                promo: "¡Chopp gratis mostrándo la App!",
                direccion: "Constitución e/ Mcal. Estigarribia",
                imagen: "https://images.unsplash.com/photo-1514933651103-005eec06c04b?q=80&w=500",
                linkMapa: "https://waze.com/ul?q=Constitución%20e/%20Mcal.%20Estigarribia,%20Asunción"
            },
            {
                nombre: "Pizzería La Kuña - Paseo Galería",
                categoria: "pizza",
                tag: "Pizzas a la Leña",
                promo: "10% OFF pagando en efectivo",
                direccion: "Paseo La Galería, Piso 2",
                imagen: "https://images.unsplash.com/photo-1513104890138-7c749659a591?q=80&w=500",
                linkMapa: "https://waze.com/ul?q=Paseo%20La%20Galería,%20Asunción"
            },
            {
                nombre: "Café Mandi'o - Centro",
                categoria: "cafe",
                tag: "Cafetería y Chipa",
                promo: "Chipa Guazú de regalo con tu café",
                direccion: "Palma e/ Chile",
                imagen: "https://images.unsplash.com/photo-1509042239860-f550ce710b93?q=80&w=500",
                linkMapa: "https://waze.com/ul?q=Palma%20e/%20Chile,%20Asunción"
            }
        ];

        const feedContainer = document.getElementById('localesFeed');
        const searchInput = document.getElementById('searchInput');

        // Función para renderizar los locales en la pantalla
        function displayLocales(lista) {
            feedContainer.innerHTML = '';
            if(lista.length === 0) {
                feedContainer.innerHTML = `<p style="text-align:center; color:gray; padding:40px;">No encontramos locales que coincidan. ¡Probá otra búsqueda!</p>`;
                return;
            }
            
            lista.forEach(local => {
                const card = document.createElement('div');
                card.className = 'card';
                card.innerHTML = `
                    <div class="card-img" style="background-image: url('${local.imagen}')">
                        <div class="promo-badge">${local.promo}</div>
                    </div>
                    <div class="card-content">
                        <div class="card-tag">${local.tag}</div>
                        <div class="card-title">${local.nombre}</div>
                        <div class="card-info">📍 ${local.direccion}</div>
                        <a href="${local.linkMapa}" target="_blank" class="card-btn">¿Cómo llegar en Waze?</a>
                    </div>
                `;
                feedContainer.appendChild(card);
            });
        }

        // Buscador funcional en tiempo real
        searchInput.addEventListener('input', (e) => {
            const term = e.target.value.toLowerCase();
            const filtrados = locales.filter(l => 
                l.nombre.toLowerCase().includes(term) || 
                l.tag.toLowerCase().includes(term) ||
                l.promo.toLowerCase().includes(term)
            );
            displayLocales(filtrados);
        });

        // Filtros por botones de categoría
        function filterCategory(cat) {
            // Cambiar estado activo de los botones
            const botones = document.querySelectorAll('.filter-btn');
            botones.forEach(btn => btn.classList.remove('active'));
            event.target.classList.add('active');

            if(cat === 'todos') {
                displayLocales(locales);
            } else {
                const filtrados = locales.filter(l => l.categoria === cat);
                displayLocales(filtrados);
            }
        }

        // Carga inicial
        displayLocales(locales);
    </script>
</body>
</html>
