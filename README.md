<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Baile & Salud - Muévete, Vive, Siente</title>
    <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        :root {
            --primary-pink: #ff006e;
            --primary-blue: #0099ff;
            --dark: #1a1a2e;
            --light: #ffffff;
            --glass-bg: rgba(255, 255, 255, 0.1);
            --glass-border: rgba(255, 255, 255, 0.2);
        }

        body {
            font-family: 'Poppins', sans-serif;
            overflow-x: hidden;
            position: relative;
            background: var(--dark);
        }

        /* FONDO ANIMADO CON GRADIENTE Y PARTÍCULAS */
        .animated-background {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            background: linear-gradient(45deg, var(--primary-pink), var(--primary-blue));
            background-size: 400% 400%;
            animation: gradientShift 15s ease infinite;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        .particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            overflow: hidden;
        }

        .particle {
            position: absolute;
            width: 4px;
            height: 4px;
            background: rgba(255, 255, 255, 0.6);
            border-radius: 50%;
            animation: float linear infinite;
        }

        @keyframes float {
            0% {
                transform: translateY(100vh) translateX(0);
                opacity: 0;
            }
            10% {
                opacity: 1;
            }
            90% {
                opacity: 1;
            }
            100% {
                transform: translateY(-100px) translateX(100px);
                opacity: 0;
            }
        }

        /* HEADER CON EFECTO VIDRIO */
        header {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            padding: 1.5rem 5%;
            background: var(--glass-bg);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            border-bottom: 1px solid var(--glass-border);
            z-index: 1000;
            display: flex;
            justify-content: space-between;
            align-items: center;
            transition: all 0.3s ease;
        }

        header.scrolled {
            background: rgba(255, 255, 255, 0.15);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
        }

        .logo {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 2rem;
            color: var(--light);
            letter-spacing: 3px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }

        .logo span {
            color: var(--primary-pink);
        }

        /* MENÚ HAMBURGUESA */
        .hamburger {
            display: flex;
            flex-direction: column;
            gap: 6px;
            cursor: pointer;
            z-index: 1001;
            transition: transform 0.3s ease;
        }

        .hamburger:hover {
            transform: scale(1.1);
        }

        .hamburger span {
            width: 30px;
            height: 3px;
            background: var(--light);
            border-radius: 3px;
            transition: all 0.3s ease;
        }

        .hamburger.active span:nth-child(1) {
            transform: rotate(45deg) translate(9px, 9px);
        }

        .hamburger.active span:nth-child(2) {
            opacity: 0;
        }

        .hamburger.active span:nth-child(3) {
            transform: rotate(-45deg) translate(9px, -9px);
        }

        /* MENÚ LATERAL */
        .menu-overlay {
            position: fixed;
            top: 0;
            right: -100%;
            width: 100%;
            max-width: 400px;
            height: 100vh;
            background: rgba(26, 26, 46, 0.95);
            backdrop-filter: blur(20px);
            -webkit-backdrop-filter: blur(20px);
            z-index: 999;
            transition: right 0.4s cubic-bezier(0.68, -0.55, 0.265, 1.55);
            padding: 100px 40px;
            box-shadow: -5px 0 30px rgba(0, 0, 0, 0.3);
        }

        .menu-overlay.active {
            right: 0;
        }

        .menu-overlay ul {
            list-style: none;
        }

        .menu-overlay ul li {
            margin: 30px 0;
            opacity: 0;
            transform: translateX(50px);
            animation: slideIn 0.5s forwards;
        }

        .menu-overlay.active ul li:nth-child(1) { animation-delay: 0.1s; }
        .menu-overlay.active ul li:nth-child(2) { animation-delay: 0.2s; }
        .menu-overlay.active ul li:nth-child(3) { animation-delay: 0.3s; }
        .menu-overlay.active ul li:nth-child(4) { animation-delay: 0.4s; }

        @keyframes slideIn {
            to {
                opacity: 1;
                transform: translateX(0);
            }
        }

        .menu-overlay ul li a {
            color: var(--light);
            text-decoration: none;
            font-size: 1.8rem;
            font-weight: 600;
            font-family: 'Bebas Neue', sans-serif;
            letter-spacing: 2px;
            transition: all 0.3s ease;
            display: inline-block;
        }

        .menu-overlay ul li a:hover {
            color: var(--primary-pink);
            transform: translateX(10px);
        }

        /* SECCIONES */
        section {
            min-height: 80vh;
            width: 100%;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 100px 5%;
            scroll-snap-align: start;
        }

        .section-content {
            width: 100%;
            max-width: 1400px;
            height: 80vh;
            position: relative;
            border-radius: 20px;
            overflow: hidden;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
        }

        /* CARRUSEL SECTION 1 */
        .carousel-container {
            width: 100%;
            height: 100%;
            position: relative;
            cursor: grab;
        }

        .carousel-container:active {
            cursor: grabbing;
        }

        .carousel-track {
            display: flex;
            height: 100%;
            transition: transform 0.5s ease;
        }

        .carousel-slide {
            min-width: 100%;
            height: 100%;
            position: relative;
            background-size: cover;
            background-position: center;
        }

        .slide-overlay {
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            padding: 40px;
            background: linear-gradient(to top, rgba(0, 0, 0, 0.8), transparent);
        }

        .slide-overlay h2 {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 3.5rem;
            color: var(--light);
            margin-bottom: 10px;
            letter-spacing: 3px;
        }

        .slide-overlay p {
            color: rgba(255, 255, 255, 0.9);
            font-size: 1.2rem;
            max-width: 600px;
        }

        /* CONTROLES DEL CARRUSEL */
        .carousel-controls {
            position: absolute;
            bottom: 30px;
            right: 30px;
            display: flex;
            gap: 15px;
            z-index: 10;
        }

        .carousel-btn {
            width: 50px;
            height: 50px;
            border: none;
            background: var(--glass-bg);
            backdrop-filter: blur(10px);
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--light);
            font-size: 1.5rem;
            transition: all 0.3s ease;
            border: 2px solid var(--glass-border);
        }

        .carousel-btn:hover {
            background: var(--primary-pink);
            transform: scale(1.1);
        }

        .carousel-indicators {
            position: absolute;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            display: flex;
            gap: 10px;
        }

        .indicator {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.4);
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .indicator.active {
            background: var(--primary-pink);
            width: 30px;
            border-radius: 6px;
        }

        /* VIDEO SECTIONS 2, 3, 4 */
        .video-section {
            width: 100%;
            height: 100%;
            position: relative;
            background-size: cover;
            background-position: center;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .video-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.4);
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all 0.3s ease;
        }

        .play-btn {
            width: 100px;
            height: 100px;
            border: 4px solid var(--light);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s ease;
            background: var(--glass-bg);
            backdrop-filter: blur(10px);
        }

        .play-btn:hover {
            transform: scale(1.2);
            background: var(--primary-pink);
            border-color: var(--primary-pink);
        }

        .play-btn::after {
            content: '';
            width: 0;
            height: 0;
            border-left: 30px solid var(--light);
            border-top: 20px solid transparent;
            border-bottom: 20px solid transparent;
            margin-left: 8px;
        }

        video {
            width: 100%;
            height: 100%;
            object-fit: cover;
            display: none;
        }

        video.playing {
            display: block;
        }

        .video-info {
            position: absolute;
            bottom: 40px;
            left: 40px;
            color: var(--light);
        }

        .video-info h3 {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 2.5rem;
            margin-bottom: 10px;
            letter-spacing: 2px;
        }

        .video-info p {
            font-size: 1.1rem;
            opacity: 0.9;
        }

        /* FOOTER */
        footer {
            background: rgba(26, 26, 46, 0.95);
            padding: 60px 5%;
            color: var(--light);
        }

        .footer-content {
            max-width: 1400px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 40px;
        }

        .footer-section h4 {
            font-family: 'Bebas Neue', sans-serif;
            font-size: 1.8rem;
            margin-bottom: 20px;
            letter-spacing: 2px;
            color: var(--primary-pink);
        }

        .footer-section a {
            color: rgba(255, 255, 255, 0.8);
            text-decoration: none;
            display: flex;
            align-items: center;
            gap: 10px;
            margin: 15px 0;
            transition: all 0.3s ease;
        }

        .footer-section a:hover {
            color: var(--primary-pink);
            transform: translateX(5px);
        }

        .social-icons {
            display: flex;
            gap: 20px;
            margin-top: 20px;
        }

        .social-icons a {
            width: 50px;
            height: 50px;
            border: 2px solid var(--glass-border);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
            transition: all 0.3s ease;
        }

        .social-icons a:hover {
            background: var(--primary-pink);
            border-color: var(--primary-pink);
            transform: translateY(-5px);
        }

        .footer-bottom {
            text-align: center;
            margin-top: 50px;
            padding-top: 30px;
            border-top: 1px solid var(--glass-border);
            color: rgba(255, 255, 255, 0.6);
        }

        /* RESPONSIVE */
        @media (max-width: 768px) {
            .logo {
                font-size: 1.5rem;
            }

            section {
                padding: 80px 3%;
            }

            .section-content {
                height: 70vh;
            }

            .slide-overlay h2 {
                font-size: 2rem;
            }

            .slide-overlay p {
                font-size: 1rem;
            }

            .menu-overlay ul li a {
                font-size: 1.5rem;
            }

            .video-info h3 {
                font-size: 1.8rem;
            }

            .carousel-controls {
                bottom: 15px;
                right: 15px;
            }

            .carousel-btn {
                width: 40px;
                height: 40px;
            }

            .play-btn {
                width: 80px;
                height: 80px;
            }

            .footer-content {
                grid-template-columns: 1fr;
                text-align: center;
            }

            .social-icons {
                justify-content: center;
            }
        }

        @media (max-width: 480px) {
            header {
                padding: 1rem 4%;
            }

            .section-content {
                border-radius: 15px;
                height: 65vh;
            }

            .slide-overlay {
                padding: 20px;
            }

            .slide-overlay h2 {
                font-size: 1.5rem;
            }

            .video-info {
                bottom: 20px;
                left: 20px;
            }
        }
    </style>
</head>
<body>
    <!-- Fondo animado con partículas -->
    <div class="animated-background"></div>
    <div class="particles" id="particles"></div>

    <!-- Header con efecto vidrio -->
    <header id="header">
        <div class="logo">BAILE<span>&</span>SALUD</div>
        <div class="hamburger" id="hamburger">
            <span></span>
            <span></span>
            <span></span>
        </div>
    </header>

    <!-- Menú lateral -->
    <div class="menu-overlay" id="menuOverlay">
        <ul>
            <li><a href="#section1" class="menu-link">Inicio</a></li>
            <li><a href="#section2" class="menu-link">Salsa & Ritmo</a></li>
            <li><a href="#section3" class="menu-link">Fitness Dance</a></li>
            <li><a href="#section4" class="menu-link">Ballet Clásico</a></li>
        </ul>
    </div>

    <!-- SECCIÓN 1: CARRUSEL -->
    <section id="section1">
        <div class="section-content">
            <div class="carousel-container" id="carousel">
                <div class="carousel-track" id="carouselTrack">
                    <div class="carousel-slide" style="background: linear-gradient(rgba(255, 0, 110, 0.3), rgba(0, 0, 0, 0.5)), url('https://images.unsplash.com/photo-1508700929628-666bc8bd84ea?w=1200');">
                        <div class="slide-overlay">
                            <h2>Baila y Transforma tu Vida</h2>
                            <p>El baile es más que movimiento, es una expresión del alma que transforma tu cuerpo y mente.</p>
                        </div>
                    </div>
                    <div class="carousel-slide" style="background: linear-gradient(rgba(0, 153, 255, 0.3), rgba(0, 0, 0, 0.5)), url('https://images.unsplash.com/photo-1518834107812-67b0b7c58434?w=1200');">
                        <div class="slide-overlay">
                            <h2>Salud en Movimiento</h2>
                            <p>Cada paso, cada giro, cada ritmo fortalece tu corazón y libera tu espíritu.</p>
                        </div>
                    </div>
                    <div class="carousel-slide" style="background: linear-gradient(rgba(255, 0, 110, 0.3), rgba(0, 0, 0, 0.5)), url('https://images.unsplash.com/photo-1504609813442-a8924e83f76e?w=1200');">
                        <div class="slide-overlay">
                            <h2>Energía Positiva</h2>
                            <p>Descubre el poder del baile para mejorar tu estado de ánimo y tu bienestar físico.</p>
                        </div>
                    </div>
                    <div class="carousel-slide" style="background: linear-gradient(rgba(0, 153, 255, 0.3), rgba(0, 0, 0, 0.5)), url('https://images.unsplash.com/photo-1520095972714-909e91b038e5?w=1200');">
                        <div class="slide-overlay">
                            <h2>Comunidad y Conexión</h2>
                            <p>Únete a una comunidad vibrante donde el baile nos conecta a todos.</p>
                        </div>
                    </div>
                </div>
                
                <div class="carousel-controls">
                    <button class="carousel-btn" id="prevBtn">‹</button>
                    <button class="carousel-btn" id="nextBtn">›</button>
                </div>
                
                <div class="carousel-indicators" id="indicators"></div>
            </div>
        </div>
    </section>

    <!-- SECCIÓN 2: VIDEO SALSA -->
    <section id="section2">
        <div class="section-content">
            <div class="video-section" style="background-image: url('https://images.unsplash.com/photo-1504609813442-a8924e83f76e?w=1200');">
                <div class="video-overlay" id="videoOverlay2">
                    <div class="play-btn" onclick="playVideo('video2', 'videoOverlay2')"></div>
                </div>
                <video id="video2" controls>
                    <source src="1.mp4" type="video/mp4">
                    Tu navegador no soporta el elemento de video.
                </video>
                <div class="video-info">
                    <h3>Salsa & Ritmo Latino</h3>
                    <p>Siente la pasión del Caribe</p>
                </div>
            </div>
        </div>
    </section>

    <!-- SECCIÓN 3: VIDEO FITNESS -->
    <section id="section3">
        <div class="section-content">
            <div class="video-section" style="background-image: url('https://images.unsplash.com/photo-1518834107812-67b0b7c58434?w=1200');">
                <div class="video-overlay" id="videoOverlay3">
                    <div class="play-btn" onclick="playVideo('video3', 'videoOverlay3')"></div>
                </div>
                <video id="video3" controls>
                    <source src="2.mp4" type="video/mp4">
                    Tu navegador no soporta el elemento de video.
                </video>
                <div class="video-info">
                    <h3>Fitness Dance</h3>
                    <p>Quema calorías mientras te diviertes</p>
                </div>
            </div>
        </div>
    </section>

    <!-- SECCIÓN 4: VIDEO BALLET -->
    <section id="section4">
        <div class="section-content">
            <div class="video-section" style="background-image: url('https://images.unsplash.com/photo-1508700929628-666bc8bd84ea?w=1200');">
                <div class="video-overlay" id="videoOverlay4">
                    <div class="play-btn" onclick="playVideo('video4', 'videoOverlay4')"></div>
                </div>
                <video id="video4" controls>
                    <source src="3.mp4" type="video/mp4">
                    Tu navegador no soporta el elemento de video.
                </video>
                <div class="video-info">
                    <h3>Ballet Clásico</h3>
                    <p>Elegancia y disciplina en cada movimiento</p>
                </div>
            </div>
        </div>
    </section>

    <!-- FOOTER -->
    <footer>
        <div class="footer-content">
            <div class="footer-section">
                <h4>Contacto</h4>
                <a href="tel:+34123456789">📞 +34 123 456 789</a>
                <a href="tel:+34987654321">📞 +34 987 654 321</a>
                <a href="mailto:info@bailesalud.com">✉️ info@bailesalud.com</a>
            </div>
            
            <div class="footer-section">
                <h4>Horarios</h4>
                <p>Lunes - Viernes: 10:00 - 21:00</p>
                <p>Sábados: 10:00 - 18:00</p>
                <p>Domingos: Cerrado</p>
            </div>
            
            <div class="footer-section">
                <h4>Síguenos</h4>
                <div class="social-icons">
                    <a href="https://facebook.com" target="_blank">f</a>
                    <a href="https://instagram.com" target="_blank">📷</a>
                    <a href="https://twitter.com" target="_blank">🐦</a>
                    <a href="https://youtube.com" target="_blank">▶️</a>
                    <a href="https://tiktok.com" target="_blank">🎵</a>
                </div>
            </div>
        </div>
        
        <div class="footer-bottom">
            <p>&copy; 2026 Baile & Salud. Todos los derechos reservados. Diseñado con ❤️ y pasión por el movimiento.</p>
        </div>
    </footer>

    <script>
        // PARTÍCULAS ALEATORIAS
        function createParticles() {
            const particlesContainer = document.getElementById('particles');
            const particleCount = 50;

            for (let i = 0; i < particleCount; i++) {
                const particle = document.createElement('div');
                particle.classList.add('particle');
                
                const size = Math.random() * 4 + 2;
                particle.style.width = size + 'px';
                particle.style.height = size + 'px';
                
                particle.style.left = Math.random() * 100 + '%';
                particle.style.animationDuration = (Math.random() * 10 + 10) + 's';
                particle.style.animationDelay = Math.random() * 5 + 's';
                
                particlesContainer.appendChild(particle);
            }
        }

        createParticles();

        // HEADER SCROLL EFFECT
        window.addEventListener('scroll', () => {
            const header = document.getElementById('header');
            if (window.scrollY > 100) {
                header.classList.add('scrolled');
            } else {
                header.classList.remove('scrolled');
            }
        });

        // MENÚ HAMBURGUESA
        const hamburger = document.getElementById('hamburger');
        const menuOverlay = document.getElementById('menuOverlay');
        const menuLinks = document.querySelectorAll('.menu-link');

        hamburger.addEventListener('click', () => {
            hamburger.classList.toggle('active');
            menuOverlay.classList.toggle('active');
        });

        menuLinks.forEach(link => {
            link.addEventListener('click', () => {
                hamburger.classList.remove('active');
                menuOverlay.classList.remove('active');
            });
        });

        // CARRUSEL
        const track = document.getElementById('carouselTrack');
        const slides = document.querySelectorAll('.carousel-slide');
        const prevBtn = document.getElementById('prevBtn');
        const nextBtn = document.getElementById('nextBtn');
        const indicatorsContainer = document.getElementById('indicators');
        const carousel = document.getElementById('carousel');

        let currentIndex = 0;
        let autoplayInterval;
        let isAutoPlaying = true;
        let startX = 0;
        let isDragging = false;

        // Crear indicadores
        slides.forEach((_, index) => {
            const indicator = document.createElement('div');
            indicator.classList.add('indicator');
            if (index === 0) indicator.classList.add('active');
            indicator.addEventListener('click', () => goToSlide(index));
            indicatorsContainer.appendChild(indicator);
        });

        const indicators = document.querySelectorAll('.indicator');

        function updateCarousel() {
            track.style.transform = `translateX(-${currentIndex * 100}%)`;
            indicators.forEach((indicator, index) => {
                indicator.classList.toggle('active', index === currentIndex);
            });
        }

        function goToSlide(index) {
            currentIndex = index;
            updateCarousel();
        }

        function nextSlide() {
            currentIndex = (currentIndex + 1) % slides.length;
            updateCarousel();
        }

        function prevSlide() {
            currentIndex = (currentIndex - 1 + slides.length) % slides.length;
            updateCarousel();
        }

        function startAutoplay() {
            autoplayInterval = setInterval(nextSlide, 4000);
        }

        function stopAutoplay() {
            clearInterval(autoplayInterval);
        }

        // Eventos de botones
        nextBtn.addEventListener('click', () => {
            nextSlide();
            stopAutoplay();
            isAutoPlaying = false;
        });

        prevBtn.addEventListener('click', () => {
            prevSlide();
            stopAutoplay();
            isAutoPlaying = false;
        });

        // Touch y Mouse events para detener y mover manualmente
        carousel.addEventListener('mousedown', (e) => {
            isDragging = true;
            startX = e.pageX;
            stopAutoplay();
            isAutoPlaying = false;
        });

        carousel.addEventListener('touchstart', (e) => {
            isDragging = true;
            startX = e.touches[0].pageX;
            stopAutoplay();
            isAutoPlaying = false;
        });

        carousel.addEventListener('mouseup', (e) => {
            if (!isDragging) return;
            isDragging = false;
            const endX = e.pageX;
            const diff = startX - endX;
            
            if (Math.abs(diff) > 50) {
                if (diff > 0) {
                    nextSlide();
                } else {
                    prevSlide();
                }
            }
        });

        carousel.addEventListener('touchend', (e) => {
            if (!isDragging) return;
            isDragging = false;
            const endX = e.changedTouches[0].pageX;
            const diff = startX - endX;
            
            if (Math.abs(diff) > 50) {
                if (diff > 0) {
                    nextSlide();
                } else {
                    prevSlide();
                }
            }
        });

        carousel.addEventListener('mouseleave', () => {
            isDragging = false;
        });

        // Iniciar autoplay
        startAutoplay();

        // REPRODUCCIÓN DE VIDEO
        function playVideo(videoId, overlayId) {
            const video = document.getElementById(videoId);
            const overlay = document.getElementById(overlayId);
            
            video.classList.add('playing');
            overlay.style.display = 'none';
            video.play();

            video.addEventListener('ended', () => {
                video.classList.remove('playing');
                overlay.style.display = 'flex';
            });

            video.addEventListener('pause', () => {
                if (video.currentTime === video.duration) return;
                video.classList.remove('playing');
                overlay.style.display = 'flex';
            });
        }

        // SMOOTH SCROLL
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth',
                        block: 'start'
                    });
                }
            });
        });
    </script>
</body>
</html>
