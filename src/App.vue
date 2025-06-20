<template>
  <div id="app">
    <nav class="navbar">
      <div class="nav-container">
        <div class="nav-logo">
          <h2>🎮 GameStore</h2>
        </div>
        <ul class="nav-menu" :class="{ active: isMenuOpen }" id="nav-menu">
          <li class="nav-item">
            <a href="#home" class="nav-link" @click="closeMenu">Home</a>
          </li>
          <li class="nav-item">
            <a href="#games" class="nav-link" @click="closeMenu">Games</a>
          </li>
          <li class="nav-item">
            <a href="#about" class="nav-link" @click="closeMenu">About</a>
          </li>
          <li class="nav-item">
            <a href="#contact" class="nav-link" @click="closeMenu">Contact</a>
          </li>
        </ul>
        <div class="nav-toggle" @click="toggleMenu" :aria-expanded="isMenuOpen ? 'true' : 'false'" aria-controls="nav-menu">
          <span class="bar"></span>
          <span class="bar"></span>
          <span class="bar"></span>
        </div>
      </div>
    </nav>

    <section id="home" class="hero">
      <div class="hero-gradient" :style="{ background: currentGradient }"></div>
      
      <div class="hero-bg-elements">
        <div class="floating-shape shape-1" :class="{ animate: shapeAnimations }"></div>
        <div class="floating-shape shape-2" :class="{ animate: shapeAnimations }"></div>
        <div class="floating-shape shape-3" :class="{ animate: shapeAnimations }"></div>
        <div class="floating-shape shape-4" :class="{ animate: shapeAnimations }"></div>
        <div class="floating-shape shape-5" :class="{ animate: shapeAnimations }"></div>
        <div class="floating-shape shape-6" :class="{ animate: shapeAnimations }"></div>
      </div>
      
      <div class="particles">
        <div class="particle" v-for="n in 30" :key="n" :style="getParticleStyle(n)"></div>
      </div>

      <div class="hero-main">
        <div class="hero-content">
          <div class="welcome-badge" :class="{ visible: welcomeVisible }">
            <span class="badge-icon">🎯</span>
            <span class="badge-text">Welcome to the Future of Gaming</span>
          </div>

          <h1 class="hero-title">
            <span class="title-main">Discover Your Next</span>
            <span class="title-highlight">{{ typedText }}</span>
            <span class="cursor" :class="{ blink: cursorBlink }">|</span>
          </h1>

          <p class="hero-description">
            Immerse yourself in a world of endless possibilities. From epic adventures to mind-bending puzzles, 
            find your perfect game in our carefully curated collection of premium titles.
          </p>

          <div class="hero-stats">
            <div class="stat-card" v-for="(stat, index) in heroStats" :key="index" 
                 :class="{ visible: statsVisible }" :style="{ animationDelay: index * 0.2 + 's' }">
              <div class="stat-icon">{{ stat.icon }}</div>
              <div class="stat-info">
                <div class="stat-number">{{ stat.number }}</div>
                <div class="stat-label">{{ stat.label }}</div>
              </div>
            </div>
          </div>

          <div class="hero-actions">
            <button class="cta-btn primary" @click="exploreGames">
              <span class="btn-text">Explore Games</span>
              <span class="btn-icon">🚀</span>
            </button>
            <button class="cta-btn secondary" @click="watchTrailer">
              <span class="btn-icon">▶️</span>
              <span class="btn-text">Watch Trailer</span>
            </button>
          </div>

          <div class="social-proof">
            <div class="proof-avatars">
              <div class="avatar" v-for="n in 5" :key="n">👤</div>
            </div>
            <div class="proof-text">
              <strong>50,000+</strong> gamers already joined our community
            </div>
          </div>
        </div>

        <div class="hero-visual">
          <div class="game-showcase-container">
            <div class="featured-game" :class="{ active: gameShowcaseActive }">
              <div class="game-screen">
                <div class="screen-content">
                  <div class="game-title">{{ featuredGame.title }}</div>
                  <div class="game-genre">{{ featuredGame.genre }}</div>
                  <div class="game-rating">
                    <span class="stars">{{ featuredGame.rating }}</span>
                    <span class="downloads">{{ featuredGame.downloads }} downloads</span>
                  </div>
                </div>
                <div class="screen-glow"></div>
              </div>
            </div>

            <div class="floating-games">
              <div class="game-icon-float" v-for="(game, index) in floatingGames" :key="index"
                   :style="getFloatingGameStyle(index)" @click="setFeaturedGame(game)">
                <span class="game-emoji">{{ game.icon }}</span>
                <div class="icon-pulse"></div>
              </div>
            </div>

            <div class="achievement-badges">
              <div class="badge badge-1">🏆 Best Seller</div>
              <div class="badge badge-2">⭐ Top Rated</div>
              <div class="badge badge-3">🔥 Trending</div>
            </div>
          </div>
        </div>
      </div>

      <div class="scroll-indicator" :class="{ visible: scrollIndicatorVisible }">
        <div class="scroll-mouse">
          <div class="scroll-wheel"></div>
        </div>
        <span class="scroll-text">Scroll to explore more</span>
      </div>

      <div class="hero-nav-dots">
        <div class="nav-dot" v-for="n in 3" :key="n" 
             :class="{ active: currentDot === n-1 }" @click="switchHeroContent(n-1)"></div>
      </div>
    </section>

    <section id="games" class="featured-games">
      <div class="container">
        <h2 class="section-title">Featured Games</h2>
        <div class="games-grid">
          <div class="game-card" v-for="game in games" :key="game.id">
            <div class="card-image">
              <div class="game-thumbnail">{{ game.icon }}</div>
              <div class="card-overlay">
                <button class="play-btn">Play Now</button> </div>
            </div>
            <div class="card-content">
              <h3 class="game-title">{{ game.title }}</h3>
              <p class="game-genre">{{ game.genre }}</p>
              <div class="game-rating">
                <span class="stars">{{ game.rating }}</span>
                <span class="price">Rp{{ game.price }}</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <section id="about" class="about">
      <div class="container">
        <div class="about-content">
          <div class="about-text">
            <h2>About yookaaStore</h2>
            <p>Your ultimate destination for the latest and greatest games. We offer a wide selection of games across all genres and platforms.</p>
            <div class="features">
              <div class="feature">
                <span class="feature-icon">🎯</span>
                <h4>Curated Selection</h4>
                <p>Hand-picked games from top developers</p>
              </div>
              <div class="feature">
                <span class="feature-icon">⚡</span>
                <h4>Instant Download</h4>
                <p>Get your games instantly after purchase</p>
              </div>
              <div class="feature">
                <span class="feature-icon">🛡️</span>
                <h4>Secure Payment</h4>
                <p>Safe and secure payment processing</p>
              </div>
            </div>
          </div>
          <div class="about-image">
            <div class="image-placeholder">🎮</div>
          </div>
        </div>
      </div>
    </section>

    <footer id="contact" class="footer">
      <div class="container">
        <div class="footer-content">
          <div class="footer-section">
            <h3>yookaaStore</h3>
            <p>Your premier destination for gaming excellence.</p>
            <div class="social-links">
              <a href="#" class="social-link" aria-label="Facebook">📘</a>
              <a href="#" class="social-link" aria-label="Instagram">📱</a>
              <a href="#" class="social-link" aria-label="Twitter">🐦</a>
            </div>
          </div>
          <div class="footer-section">
            <h4>Quick Links</h4>
            <ul>
              <li><a href="#home">Home</a></li>
              <li><a href="#games">Games</a></li>
              <li><a href="#about">About</a></li>
              <li><a href="#contact">Contact</a></li>
            </ul>
          </div>
          <div class="footer-section">
            <h4>Support</h4>
            <ul>
              <li><a href="#">Help Center</a></li>
              <li><a href="#">Privacy Policy</a></li>
              <li><a href="#">Terms of Service</a></li>
              <li><a href="#">Refund Policy</a></li>
            </ul>
          </div>
          <div class="footer-section">
            <h4>Contact Info</h4>
            <p>📧 ekamaulanahidayat.com</p>
            <p>📞 083897423872</p>
            <p>📍 Marpoyan Damai, RIAU</p>
          </div>
        </div>
        <div class="footer-bottom">
          <p>&copy; 2025 yookaaStore. All rights reserved.</p>
        </div>
      </div>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'GameStoreLanding',
  data() {
    return {
      isMenuOpen: false,
      
      // Hero Animation States
      welcomeVisible: false,
      statsVisible: false,
      gameShowcaseActive: false,
      scrollIndicatorVisible: false,
      shapeAnimations: false,
      
      // Typing Effect
      typedText: '',
      typeIndex: 0,
      typeTexts: ['Epic Adventure', 'Thrilling Experience', 'Gaming Journey'],
      currentTypeText: 0,
      cursorBlink: true,
      
      // Hero Content
      currentDot: 0,
      currentGradient: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
      gradients: [
        'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
        'linear-gradient(135deg, #f093fb 0%, #f5576c 100%)',
        'linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)'
      ],
      
      heroStats: [
        { icon: '🎮', number: '1000+', label: 'Games Available' },
        { icon: '👥', number: '50K+', label: 'Active Players' },
        { icon: '⭐', number: '4.9', label: 'Average Rating' },
        { icon: '🏆', number: '100+', label: 'Awards Won' }
      ],
      
      featuredGame: {
        title: 'Cyber Knights 2024',
        genre: 'Action RPG',
        rating: '⭐⭐⭐⭐⭐',
        downloads: '25K+'
      },
      
      floatingGames: [
        { icon: '🤖', title: 'Cyber Knights 2024', genre: 'Action RPG', rating: '⭐⭐⭐⭐⭐', downloads: '25K+' },
        { icon: '🐉', title: 'Dragon Quest', genre: 'Fantasy', rating: '⭐⭐⭐⭐⭐', downloads: '18K+' },
        { icon: '🚀', title: 'Space Odyssey', genre: 'Sci-Fi', rating: '⭐⭐⭐⭐⭐', downloads: '30K+' },
        { icon: '🏰', title: 'Castle Defense', genre: 'Strategy', rating: '⭐⭐⭐⭐', downloads: '12K+' },
        { icon: '🌲', title: 'Forest Adventure', genre: 'Adventure', rating: '⭐⭐⭐⭐⭐', downloads: '20K+' },
        { icon: '⚔️', title: 'Battle Arena', genre: 'Fighting', rating: '⭐⭐⭐⭐', downloads: '15K+' }
      ],
      
      games: [
        {
          id: 1,
          title: "Cyber Knights 2024",
          genre: "Action RPG",
          rating: "⭐⭐⭐⭐⭐",
          price: "49.99",
          icon: "🤖"
        },
        {
          id: 2,
          title: "Forest Quest",
          genre: "Adventure",
          rating: "⭐⭐⭐⭐⭐",
          price: "29.99",
          icon: "🌲"
        },
        {
          id: 3,
          title: "Space Odyssey",
          genre: "Sci-Fi",
          rating: "⭐⭐⭐⭐⭐",
          price: "39.99",
          icon: "🚀"
        },
        {
          id: 4,
          title: "Dragon's Realm",
          genre: "Fantasy",
          rating: "⭐⭐⭐⭐⭐",
          price: "59.99",
          icon: "🐉"
        },
        {
          id: 5,
          title: "Racing Thunder",
          genre: "Racing",
          rating: "⭐⭐⭐⭐⭐",
          price: "34.99",
          icon: "🏎️"
        },
        {
          id: 6,
          title: "Mystery Island",
          genre: "Puzzle",
          rating: "⭐⭐⭐⭐⭐",
          price: "24.99",
          icon: "🏝️"
        }
      ]
    }
  },
  
  mounted() {
    this.initializeAnimations();
    this.startTypeWriter();
  },
  
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    
    closeMenu() {
      this.isMenuOpen = false;
    },
    
    initializeAnimations() {
      // Staggered entrance animations for hero section elements
      setTimeout(() => this.welcomeVisible = true, 500);
      setTimeout(() => this.statsVisible = true, 1000);
      setTimeout(() => this.gameShowcaseActive = true, 1500);
      setTimeout(() => this.scrollIndicatorVisible = true, 2000);
      setTimeout(() => this.shapeAnimations = true, 2500);
    },
    
    startTypeWriter() {
      const typeText = () => {
        const currentText = this.typeTexts[this.currentTypeText];
        if (this.typeIndex < currentText.length) {
          this.typedText += currentText.charAt(this.typeIndex);
          this.typeIndex++;
          setTimeout(typeText, 100);
        } else {
          // Wait before erasing
          setTimeout(() => {
            this.eraseText();
          }, 2000);
        }
      };
      
      const eraseText = () => {
        if (this.typedText.length > 0) {
          this.typedText = this.typedText.slice(0, -1);
          setTimeout(eraseText, 50);
        } else {
          // Move to next text and start typing again
          this.currentTypeText = (this.currentTypeText + 1) % this.typeTexts.length;
          this.typeIndex = 0;
          setTimeout(typeText, 500);
        }
      };
      
      // Assign eraseText to this.eraseText so it can be called internally
      this.eraseText = eraseText; 
      typeText(); // Start the typing effect initially
      
      // Cursor blink effect
      setInterval(() => {
        this.cursorBlink = !this.cursorBlink;
      }, 500);
    },
    
    switchHeroContent(index) {
      this.currentDot = index;
      this.currentGradient = this.gradients[index];
      // You might want to also change featuredGame and other content based on the dot clicked
      // For demonstration, let's just cycle through some featured games as well
      this.setFeaturedGame(this.floatingGames[index % this.floatingGames.length]); 
    },
    
    exploreGames() {
      // Smooth scroll to the games section
      document.getElementById('games').scrollIntoView({ behavior: 'smooth' });
    },
    
    watchTrailer() {
      // Placeholder for watch trailer functionality
      console.log('Opening trailer...');
      alert('Trailer functionality coming soon!');
    },
    
    setFeaturedGame(game) {
      this.featuredGame = {
        title: game.title,
        genre: game.genre,
        rating: game.rating,
        downloads: game.downloads
      };
    },
    
    getParticleStyle(n) {
      return {
        left: Math.random() * 100 + '%',
        top: Math.random() * 100 + '%',
        animationDelay: Math.random() * 3 + 's',
        animationDuration: (Math.random() * 3 + 2) + 's',
        fontSize: Math.random() * 10 + 5 + 'px'
      };
    },
    
    getFloatingGameStyle(index) {
      // These angles and radius create an orbiting effect around a central point
      const angles = [0, 60, 120, 180, 240, 300];
      const radius = 120;
      const angle = angles[index] * Math.PI / 180;
      
      return {
        transform: `translate(${Math.cos(angle) * radius}px, ${Math.sin(angle) * radius}px)`,
        animationDelay: index * 0.2 + 's' // Staggered entry
      };
    }
  }
}
</script>

<style>
/* Base Styles */
body {
  margin: 0;
  font-family: 'Poppins', sans-serif;
  background-color: #0a0a0a;
  color: #f8f9fa;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

/* Global Container */
.container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 0 2rem;
}

/* --- Navbar Styles --- */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background: rgba(10, 10, 10, 0.9);
  backdrop-filter: blur(10px);
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  z-index: 1000;
  transition: all 0.3s ease;
}

.nav-container {
  max-width: 1400px;
  margin: 0 auto;
  padding: 1rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-logo h2 {
  margin: 0;
  color: white;
  font-size: 1.5rem;
}

.nav-menu {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
  gap: 2rem;
}

.nav-link {
  color: #a0a0a0;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s ease;
  position: relative;
}

.nav-link:hover {
  color: #667eea;
}

.nav-link::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 2px;
  background: #667eea;
  transition: width 0.3s ease;
}

.nav-link:hover::after {
  width: 100%;
}

.nav-toggle {
  display: none;
  flex-direction: column;
  cursor: pointer;
  padding: 0.5rem; /* Add padding for easier clicking */
}

.bar {
  width: 25px;
  height: 3px;
  background: white;
  margin: 3px 0;
  transition: 0.3s;
}

/* --- Enhanced Hero Section Styles --- */
.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  overflow: hidden;
  background: #0a0a0a;
  padding-top: 70px; /* Offset for fixed navbar */
}

.hero-gradient {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  opacity: 0.1;
  transition: all 1s ease;
}

.hero-bg-elements {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  pointer-events: none;
}

.floating-shape {
  position: absolute;
  border-radius: 50%;
  background: linear-gradient(45deg, #667eea, #764ba2);
  opacity: 0.1;
  animation: float 6s ease-in-out infinite;
}

.floating-shape.animate {
  opacity: 0.15;
}

.shape-1 { width: 100px; height: 100px; top: 10%; left: 10%; animation-delay: 0s; }
.shape-2 { width: 60px; height: 60px; top: 20%; right: 15%; animation-delay: 1s; }
.shape-3 { width: 80px; height: 80px; bottom: 20%; left: 20%; animation-delay: 2s; }
.shape-4 { width: 120px; height: 120px; top: 50%; right: 10%; animation-delay: 3s; }
.shape-5 { width: 40px; height: 40px; top: 70%; left: 50%; animation-delay: 4s; }
.shape-6 { width: 90px; height: 90px; bottom: 10%; right: 30%; animation-delay: 5s; }

.particles {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  pointer-events: none;
}

.particle {
  position: absolute;
  color: #667eea;
  opacity: 0.3;
  animation: particleFloat 4s ease-in-out infinite;
}

.particle::before {
  content: '✨';
}

.hero-main {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  max-width: 1400px;
  margin: 0 auto;
  padding: 2rem;
  position: relative;
  z-index: 2;
}

.hero-content {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 2rem;
}

.welcome-badge {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  background: rgba(102, 126, 234, 0.1);
  border: 1px solid rgba(102, 126, 234, 0.3);
  padding: 0.75rem 1.5rem;
  border-radius: 50px;
  width: fit-content;
  color: #667eea;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.6s ease;
}

.welcome-badge.visible {
  opacity: 1;
  transform: translateY(0);
}

.hero-title {
  font-size: 3.5rem;
  font-weight: 800;
  line-height: 1.1;
  color: white;
  margin: 0;
}

.title-main {
  display: block;
  color: #f8f9fa;
}

.title-highlight {
  display: block;
  background: linear-gradient(135deg, #667eea, #764ba2);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  min-height: 1.1em; /* Ensures consistent height during typing */
}

.cursor {
  color: #667eea;
  font-weight: normal;
  opacity: 1;
  transition: opacity 0.1s;
}

.cursor.blink {
  opacity: 0;
}

.hero-description {
  font-size: 1.2rem;
  color: #a0a0a0;
  line-height: 1.6;
  max-width: 500px;
}

.hero-stats {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1rem;
}

.stat-card {
  display: flex;
  align-items: center;
  gap: 1rem;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  padding: 1rem;
  border-radius: 12px;
  backdrop-filter: blur(10px);
  opacity: 0;
  transform: translateY(20px);
  animation: slideUp 0.6s ease forwards;
}

.stat-card.visible {
  opacity: 1;
  transform: translateY(0);
}

.stat-icon {
  font-size: 2rem;
}

.stat-number {
  font-size: 1.5rem;
  font-weight: 700;
  color: white;
}

.stat-label {
  font-size: 0.9rem;
  color: #a0a0a0;
}

.hero-actions {
  display: flex;
  gap: 1rem;
  margin-top: 1rem;
}

.cta-btn {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 1rem 2rem;
  border: none;
  border-radius: 50px;
  font-size: 1.1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  overflow: hidden;
  text-decoration: none; /* Ensure no underline for button as anchor */
}

.cta-btn.primary {
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
}

.cta-btn.secondary {
  background: transparent;
  color: white;
  border: 2px solid rgba(255, 255, 255, 0.3);
}

.cta-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 25px rgba(102, 126, 234, 0.3);
}

.social-proof {
  display: flex;
  align-items: center;
  gap: 1rem;
  margin-top: 2rem;
}

.proof-avatars {
  display: flex;
  margin-left: 0.5rem; /* Adjusted for better stacking */
}

.avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: linear-gradient(135deg, #667eea, #764ba2);
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: -0.5rem;
  border: 2px solid #0a0a0a;
}
.avatar:first-child {
  margin-left: 0; /* Remove negative margin for the first avatar */
}


.proof-text {
  color: #a0a0a0;
  font-size: 0.9rem;
}

.hero-visual {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
}

.game-showcase-container {
  position: relative;
  width: 100%;
  max-width: 500px; /* Constrain width for better control */
  height: 500px;
}

.featured-game {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  opacity: 0;
  transition: all 0.8s ease;
  z-index: 10; /* Ensure it's above floating icons if overlapping */
}

.featured-game.active {
  opacity: 1;
}

.game-screen {
  width: 300px;
  height: 200px;
  background: linear-gradient(135deg, #1a1a1a, #2d2d2d);
  border-radius: 20px;
  border: 3px solid #667eea;
  position: relative;
  overflow: hidden;
  box-shadow: 0 20px 40px rgba(102, 126, 234, 0.3);
}

.screen-content {
  padding: 2rem;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
  z-index: 2;
}

.game-title {
  font-size: 1.5rem;
  font-weight: 700;
  color: white;
  margin-bottom: 0.5rem;
}

.game-genre {
  color: #a0a0a0;
  margin-bottom: 1rem;
}

.game-rating {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.downloads {
  color: #667eea;
  font-size: 0.9rem;
}

.screen-glow {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: linear-gradient(45deg, rgba(102, 126, 234, 0.1), rgba(118, 75, 162, 0.1));
  animation: pulse 2s ease-in-out infinite;
}

.floating-games {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.game-icon-float {
  position: absolute; /* Keep absolute for orbiting effect */
  width: 60px;
  height: 60px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 15px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.2);
  animation: floatOrbit 8s linear infinite; /* Apply orbit animation */
}

.game-icon-float:hover {
  transform: scale(1.1) translate(var(--translateX, 0), var(--translateY, 0)); /* Scale on hover, preserve existing translate */
  background: rgba(102, 126, 234, 0.2);
}

.game-emoji {
  font-size: 1.5rem;
}

.icon-pulse {
  position: absolute;
  top: -5px;
  left: -5px;
  right: -5px;
  bottom: -5px;
  border: 2px solid #667eea;
  border-radius: 20px;
  animation: iconPulse 2s ease-in-out infinite;
}

.achievement-badges {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  pointer-events: none; /* Allow clicks through to elements below if desired */
}

.badge {
  position: absolute;
  background: linear-gradient(135deg, #667eea, #764ba2);
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 20px;
  font-size: 0.8rem;
  font-weight: 600;
  animation: badgeFloat 3s ease-in-out infinite;
  pointer-events: auto; /* Re-enable pointer events for badges if interactive */
}

.badge-1 { top: 10%; right: 20%; animation-delay: 0s; }
.badge-2 { bottom: 20%; left: 10%; animation-delay: 1s; }
.badge-3 { top: 60%; right: 10%; animation-delay: 2s; }

.scroll-indicator {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  color: #a0a0a0;
  opacity: 0;
  transition: all 0.6s ease;
  z-index: 5; /* Ensure it's above background elements */
}

.scroll-indicator.visible {
  opacity: 1;
}

.scroll-mouse {
  width: 24px;
  height: 40px;
  border: 2px solid #667eea;
  border-radius: 12px;
  position: relative;
}

.scroll-wheel {
  width: 4px;
  height: 8px;
  background: #667eea;
  border-radius: 2px;
  position: absolute;
  top: 6px;
  left: 50%;
  transform: translateX(-50%);
  animation: scrollWheel 2s ease-in-out infinite;
}

.scroll-text {
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.hero-nav-dots {
  position: absolute;
  right: 2rem;
  top: 50%;
  transform: translateY(-50%);
  display: flex;
  flex-direction: column;
  gap: 1rem;
  z-index: 5;
}

.nav-dot {
  width: 12px;
  height: 12px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.3);
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
}

.nav-dot.active {
  background: #667eea;
  transform: scale(1.2);
}

.nav-dot::before {
  content: '';
  position: absolute;
  top: -8px;
  left: -8px;
  right: -8px;
  bottom: -8px;
  border: 2px solid transparent;
  border-radius: 50%;
  transition: all 0.3s ease;
}

.nav-dot.active::before {
  border-color: rgba(102, 126, 234, 0.3);
}

/* --- Animations --- */
@keyframes float {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-20px) rotate(180deg); }
}

@keyframes particleFloat {
  0%, 100% { 
    transform: translateY(0px) rotate(0deg);
    opacity: 0.3;
  }
  50% { 
    transform: translateY(-30px) rotate(180deg);
    opacity: 0.8;
  }
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes pulse {
  0%, 100% { opacity: 0.1; }
  50% { opacity: 0.3; }
}

/* Adjusted floatOrbit to work better with individual transform from JS */
@keyframes floatOrbit {
  0% { transform: rotate(0deg) translateX(120px) rotate(0deg); }
  100% { transform: rotate(360deg) translateX(120px) rotate(-360deg); }
}

@keyframes iconPulse {
  0%, 100% { 
    opacity: 0;
    transform: scale(1);
  }
  50% { 
    opacity: 1;
    transform: scale(1.1);
  }
}

@keyframes badgeFloat {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-10px); }
}

@keyframes scrollWheel {
  0% { opacity: 1; transform: translate(-50%, 0); }
  50% { opacity: 0.3; transform: translate(-50%, 10px); }
  100% { opacity: 1; transform: translate(-50%, 0); }
}

/* --- Featured Games Section Styles --- */
.featured-games {
  padding: 5rem 0;
  background: #111;
}

.section-title {
  text-align: center;
  font-size: 2.5rem;
  color: white;
  margin-bottom: 3rem;
}

.games-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); /* Adjusted min-width for better fit */
  gap: 2rem;
}

.game-card {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 15px;
  overflow: hidden;
  transition: transform 0.3s ease, box-shadow 0.3s ease; /* Add box-shadow transition */
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.game-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
}

.card-image {
  position: relative;
  height: 200px;
  background: linear-gradient(135deg, #667eea, #764ba2);
  display: flex;
  align-items: center;
  justify-content: center;
}

.game-thumbnail {
  font-size: 4rem;
}

.card-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.card-image:hover .card-overlay {
  opacity: 1;
}

.play-btn {
  background: #667eea;
  color: white;
  border: none;
  padding: 0.8rem 1.5rem;
  border-radius: 25px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.3s ease, transform 0.3s ease;
}

.play-btn:hover {
  background: #5a6fe0;
  transform: translateY(-2px);
}

.card-content {
  padding: 1.5rem;
}

.game-title {
  color: white;
  margin: 0 0 0.5rem 0;
  font-size: 1.2rem;
}

.game-genre {
  color: #a0a0a0;
  margin: 0 0 1rem 0;
}

.game-rating {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.price {
  color: #667eea;
  font-weight: 600;
}

/* --- About Section Styles --- */
.about {
  padding: 5rem 0;
  background: #0a0a0a;
}

.about-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.about-text h2 {
  color: white;
  font-size: 2.5rem;
  margin-bottom: 1rem;
}

.about-text p {
  color: #a0a0a0;
  font-size: 1.1rem;
  line-height: 1.6;
  margin-bottom: 2rem;
}

.features {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.feature {
  display: flex;
  align-items: flex-start;
  gap: 1rem;
}

.feature-icon {
  font-size: 2rem;
}

.feature h4 {
  color: white;
  margin: 0 0 0.5rem 0;
}

.feature p {
  color: #a0a0a0;
  margin: 0;
}

.about-image {
  display: flex;
  align-items: center;
  justify-content: center;
}

.image-placeholder {
  width: 300px;
  height: 300px;
  background: linear-gradient(135deg, #667eea, #764ba2);
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 6rem;
  box-shadow: 0 20px 40px rgba(102, 126, 234, 0.3);
}

/* --- Footer Styles --- */
.footer {
  background: #111;
  padding: 3rem 0 1rem;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
}

.footer-content {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); /* Adjusted min-width */
  gap: 2rem;
  margin-bottom: 2rem;
}

.footer-section h3,
.footer-section h4 {
  color: white;
  margin-bottom: 1rem;
}

.footer-section p,
.footer-section li {
  color: #a0a0a0;
  margin-bottom: 0.5rem;
}

.footer-section ul {
  list-style: none;
  padding: 0;
}

.footer-section a {
  color: #a0a0a0;
  text-decoration: none;
  transition: color 0.3s ease;
}

.footer-section a:hover {
  color: #667eea;
}

.social-links {
  display: flex;
  gap: 1rem;
  margin-top: 1rem;
}

.social-link {
  width: 40px;
  height: 40px;
  background: rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.2rem;
  transition: all 0.3s ease;
  text-decoration: none;
}

.social-link:hover {
  background: #667eea;
  transform: translateY(-2px);
}

.footer-bottom {
  text-align: center;
  padding-top: 2rem;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  color: #a0a0a0;
}

/* --- Responsive Design --- */
@media screen and (max-width: 992px) {
  .hero-main {
    grid-template-columns: 1fr; /* Stack content on smaller desktops/tablets */
    gap: 3rem;
  }
  .hero-content {
    align-items: center; /* Center text content */
    text-align: center;
  }
  .hero-description {
    max-width: 600px; /* Allow description to be wider when centered */
  }
  .welcome-badge {
    margin: 0 auto; /* Center the badge */
  }
  .hero-actions {
    justify-content: center; /* Center buttons */
  }
  .social-proof {
    justify-content: center; /* Center social proof */
  }
  .hero-visual {
    padding-bottom: 5rem; /* Add padding to prevent overlap with scroll indicator */
  }
  .hero-nav-dots {
    flex-direction: row; /* Dots in a row at the bottom center */
    left: 50%;
    transform: translateX(-50%);
    bottom: 2rem;
    top: auto;
    padding-top: 2rem;
  }
}

@media screen and (max-width: 768px) {
  .nav-menu {
    position: fixed;
    left: -100%;
    top: 65px; /* Adjust based on navbar height */
    flex-direction: column;
    background: rgba(10, 10, 10, 0.98); /* Slightly less transparent */
    width: 100%;
    text-align: center;
    transition: 0.3s;
    backdrop-filter: blur(10px);
    padding: 2rem 0;
    height: calc(100vh - 65px); /* Take full height below navbar */
    justify-content: center; /* Center menu items vertically */
    gap: 1.5rem;
  }
  
  .nav-menu.active {
    left: 0;
  }
  
  .nav-toggle {
    display: flex;
  }

  /* Hamburger icon animation */
  .nav-toggle.active .bar:nth-child(1) {
    transform: translateY(8px) rotate(45deg);
  }
  .nav-toggle.active .bar:nth-child(2) {
    opacity: 0;
  }
  .nav-toggle.active .bar:nth-child(3) {
    transform: translateY(-8px) rotate(-45deg);
  }

  .hero {
    padding-top: 80px; /* More padding for smaller screens */
  }
  
  .hero-title {
    font-size: 2.8rem; /* Adjusted for tablet */
  }
  
  .hero-stats {
    grid-template-columns: 1fr; /* Stack stats vertically */
  }
  
  .hero-actions {
    flex-direction: column; /* Stack buttons vertically */
    align-items: center;
  }
  
  .game-showcase-container {
    height: 350px; /* Adjust height for tablet */
  }
  
  .featured-game {
    transform: translate(-50%, -50%) scale(0.9); /* Slightly smaller on tablets */
  }
  
  .game-screen {
    width: 280px;
    height: 180px;
  }
  
  .floating-games {
    /* For tablets, we might want a less chaotic arrangement or no orbit */
    position: relative; /* Make them flow naturally */
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    transform: none; /* Remove previous transform */
    margin-top: 2rem; /* Space below featured game */
  }
  
  .game-icon-float {
    position: relative; /* Let them flow with flexbox */
    margin: 0.5rem; /* Add consistent margin */
    animation: float 4s ease-in-out infinite; /* Apply simple float, not orbit */
    transform: none !important; /* Override inline transform from JS for mobile layout */
  }
  
  .hero-nav-dots {
    bottom: 1rem; /* Adjust position */
  }
  
  .about-content {
    grid-template-columns: 1fr; /* Stack about content */
    text-align: center;
  }
  
  .features {
    align-items: center; /* Center features */
  }
  
  .feature {
    text-align: center;
    flex-direction: column;
  }
  .about-image {
    margin-top: 2rem;
  }
}

@media screen and (max-width: 480px) {
  .hero-title {
    font-size: 2rem; /* Smaller title for phones */
  }
  
  .hero-description {
    font-size: 1rem;
  }
  
  .cta-btn {
    padding: 0.8rem 1.5rem;
    font-size: 1rem;
  }
  
  .game-screen {
    width: 240px;
    height: 140px;
  }
  .game-title {
    font-size: 1.3rem;
  }
  .floating-shape {
    display: none; /* Hide floating shapes on very small screens for performance */
  }
  .particles {
    display: none; /* Hide particles for performance on small screens */
  }
  .scroll-indicator {
    display: none; /* Hide scroll indicator if space is tight */
  }
  .game-showcase-container {
    height: 300px;
  }
  .badge {
    font-size: 0.7rem;
    padding: 0.4rem 0.8rem;
  }
  .image-placeholder {
    width: 250px;
    height: 250px;
    font-size: 4rem;
  }
  .footer-content {
    grid-template-columns: 1fr; /* Stack footer sections */
    text-align: center;
  }
  .social-links {
    justify-content: center;
  }
}
</style>

