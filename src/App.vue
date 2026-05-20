<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

// IMPORT DES IMAGES DEPUIS /assets
import img1 from './assets/img/restaurant1.jpg'
import img2 from './assets/img/restaurant2.jpg'
import img3 from './assets/img/restaurant3.jpg'
import img4 from './assets/img/restaurant4.jpg'
import img5 from './assets/img/restaurant5.jpg'

// Tableau des images
const images = [img1, img2, img3, img4, img5]

// Image actuellement affichée
const currentImage = ref(images[0])

let currentIndex = 0
let interval = null

// Changement automatique toutes les 5 secondes
onMounted(() => {
  interval = setInterval(() => {
    currentIndex = (currentIndex + 1) % images.length
    currentImage.value = images[currentIndex]
  }, 5000)
})

// Nettoyage
onBeforeUnmount(() => {
  clearInterval(interval)
})

const showMenu = ref(false)

const openMenu = () => {
  window.open('https://maps.app.goo.gl/UuLmcp3S9pscDbn88', '_blank')
}
</script>

<template>
  <div class="home-page">
    <!-- BANDEAU DÉFILANT -->
    <div class="scroll-banner">
      <div class="scroll-text">
        ⚠️ Mettez sur ce bandeau le texte que vous voulez pour informer vos clients !
      </div>
    </div>

    <!-- Hero Section -->
    <section class="hero">
      <img class="hero-image" :src="currentImage" alt="Restaurant" />

      <div class="overlay"></div>

      <div class="hero-content">
        <h1 class="name">La Cantine de Juliette</h1>
        <p>Une expérience culinaire unique dans les Landes</p>

        <div class="buttons">
          <button class="primary-btn">Réservations uniquement par téléphone</button>

          <!-- Bouton Menu -->
          <button class="secondary-btn" @click="openMenu">Voir le Menu</button>
        </div>
      </div>
    </section>

    <!-- MENU -->
    <transition name="fade">
      <section v-if="showMenu" class="menu-section">
        <h2>Notre Menu</h2>

        <div class="menu-grid">
          <div class="menu-card">
            <h3>🍝 Pâtes Carbonara</h3>
            <p>Pâtes fraîches, crème, lardons, parmesan.</p>
            <span>14€</span>
          </div>

          <div class="menu-card">
            <h3>🥩 Entrecôte Grillée</h3>
            <p>Servie avec pommes de terre et sauce maison.</p>
            <span>22€</span>
          </div>

          <div class="menu-card">
            <h3>🍕 Pizza Burrata</h3>
            <p>Tomate, mozzarella, burrata crémeuse, basilic.</p>
            <span>16€</span>
          </div>

          <div class="menu-card">
            <h3>🍰 Tiramisu</h3>
            <p>Recette italienne traditionnelle au café.</p>
            <span>8€</span>
          </div>
        </div>
      </section>
    </transition>

    <!-- ABOUT -->
    <section class="about">
      <h2>Bienvenue dans notre restaurant</h2>
      <p>
        Découvrez une cuisine raffinée préparée avec des ingrédients frais et locaux dans une
        ambiance chaleureuse et moderne.
      </p>
    </section>

    <!-- FOOTER -->
    <footer class="footer">
      <div class="footer-content">
        <!-- INFOS -->
        <div class="footer-top">
          <!-- Adresse -->
          <div class="footer-info">
            <h3>📍 Adresse</h3>
            <p>5 Rue Victor Hugo, 40400 Tartas</p>

            <h3>📞 Téléphone</h3>
            <p>05 24 62 52 86</p>
          </div>

          <!-- Horaires -->
          <div class="opening-hours">
            <h3>🕒 Horaires d'ouverture</h3>

            <ul>
              <li>Lundi : Fermé</li>
              <li>Mardi : 12h00 - 14h00</li>
              <li>Mercredi : 12h00 - 14h00</li>
              <li>Jeudi : 12h00 - 14h00</li>
              <li>Vendredi : 12h00 - 14h00 / 18h00 - 22h00</li>
              <li>Samedi : 12h00 - 14h00 / 18h00 - 22h00</li>
              <li>Dimanche : Fermé</li>
            </ul>
          </div>
        </div>

        <!-- GOOGLE MAPS -->
        <div class="map-container">
          <iframe
            src="https://www.google.com/maps?q=5+Rue+Victor+Hugo,+40400+Tartas&output=embed"
            width="100%"
            height="300"
            style="border: 0"
            allowfullscreen=""
            loading="lazy"
          >
          </iframe>
        </div>
      </div>

      <p class="copyright">© 2026 La Cantine de Juliette - Tous droits réservés</p>

      <p class="creator">Créé par : Bruno DUPUIS</p>
    </footer>
  </div>
</template>

<style scoped>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.home-page {
  font-family: Arial, sans-serif;
  color: white;
}
/* BANDEAU DÉFILANT */

.scroll-banner {
  position: absolute;
  top: 0;
  width: 100%;
  background: #d4a373;
  overflow: hidden;
  z-index: 20;
  height: 45px;
  display: flex;
  align-items: center;
}

.scroll-text {
  white-space: nowrap;
  color: white;
  font-weight: bold;
  font-size: 1rem;
  padding-left: 100%;
  animation: scrollText 18s linear infinite;
}

/* Animation défilement */

@keyframes scrollText {
  0% {
    transform: translateX(0%);
  }

  100% {
    transform: translateX(-100%);
  }
}

/* Décale le contenu du hero */
.hero-content {
  position: absolute;
  top: 55%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  width: 90%;
}

/* Responsive */

@media (max-width: 768px) {
  .scroll-text {
    font-size: 0.9rem;
  }

  .scroll-banner {
    height: 40px;
  }
}

/* HERO */

.hero {
  position: relative;
  height: 100vh;
  overflow: hidden;
}

.hero-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
/* IMAGE HERO */

.hero-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  animation: fadeImage 1s ease-in-out;
}

/* Transition douce */

@keyframes fadeImage {
  from {
    opacity: 0.4;
  }

  to {
    opacity: 1;
  }
}

.overlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.45);
}

.hero-content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  width: 90%;
}

.hero-content h1 {
  font-size: 5rem;
  margin-bottom: 1rem;
  letter-spacing: 3px;
}

.hero-content p {
  font-size: 1.5rem;
  margin-bottom: 2rem;
}

/* BUTTONS */

.buttons {
  display: flex;
  justify-content: center;
  gap: 1rem;
}

button {
  padding: 14px 28px;
  border: none;
  cursor: pointer;
  font-size: 1rem;
  border-radius: 30px;
  transition: 0.3s ease;
}

.primary-btn {
  background-color: #d4a373;
  color: white;
}

.primary-btn:hover {
  background-color: #c58b55;
}

.secondary-btn {
  background-color: transparent;
  border: 2px solid white;
  color: white;
}

.secondary-btn:hover {
  background-color: white;
  color: black;
}

/* MENU */

.menu-section {
  background: #1a1a1a;
  padding: 80px 20px;
  text-align: center;
}

.menu-section h2 {
  font-size: 3rem;
  margin-bottom: 50px;
}

.menu-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 25px;
  max-width: 1100px;
  margin: auto;
}

.menu-card {
  background: #2a2a2a;
  padding: 30px;
  border-radius: 20px;
  transition: transform 0.3s ease;
}

.menu-card:hover {
  transform: translateY(-8px);
}

.menu-card h3 {
  margin-bottom: 15px;
  color: #d4a373;
}

.menu-card p {
  color: #ddd;
  margin-bottom: 15px;
  line-height: 1.5;
}

.menu-card span {
  font-size: 1.2rem;
  font-weight: bold;
}

/* ABOUT */

.about {
  background: #111;
  padding: 80px 20px;
  text-align: center;
}

.about h2 {
  font-size: 2.5rem;
  margin-bottom: 20px;
}

.about p {
  max-width: 700px;
  margin: auto;
  font-size: 1.1rem;
  line-height: 1.8;
  color: #ddd;
}

/* FOOTER */

.footer {
  background: #000;
  padding: 60px 20px 20px;
}

.footer-content {
  max-width: 1200px;
  margin: auto;
}

/* BLOCS DU HAUT */

.footer-top {
  display: flex;
  justify-content: center;
  align-items: flex-start;
  gap: 80px;
  flex-wrap: wrap;
  text-align: center;
  margin-bottom: 50px;
}

.footer-info,
.opening-hours {
  min-width: 280px;
}

.footer-info h3,
.opening-hours h3 {
  color: #d4a373;
  margin-bottom: 15px;
}

.footer-info p,
.opening-hours li {
  color: #ddd;
  margin-bottom: 10px;
  line-height: 1.6;
}

.opening-hours ul {
  list-style: none;
  padding: 0;
}

/* MAP */

.map-container {
  width: 100%;
  max-width: 900px;
  margin: auto;
}

.map-container iframe {
  border-radius: 20px;
}

/* COPYRIGHT */

.copyright {
  text-align: center;
  margin-top: 40px;
  color: #888;
  font-size: 0.9rem;
}

.creator {
  text-align: center;
  margin-top: 10px;
  color: #666;
  font-size: 0.9rem;
  letter-spacing: 1px;
}

/* RESPONSIVE */

@media (max-width: 768px) {
  .footer-top {
    flex-direction: column;
    gap: 40px;
  }
}
@media (max-width: 500px) {
  .hero-content h1 {
    font-size: 50px;
  }
}
</style>
