<template>
  <div id="app">
    <Navbar 
      :is-menu-open="isMenuOpen" 
      @toggle-menu="toggleMenu"
      @close-menu="closeMenu"
    />

    <Carousel
      :current-gradient="currentGradient"
      :shape-animations="shapeAnimations"
      :welcome-visible="welcomeVisible"
      :stats-visible="statsVisible"
      :game-showcase-active="gameShowcaseActive"
      :scroll-indicator-visible="scrollIndicatorVisible"
      :typed-text="typedText"
      :cursor-blink="cursorBlink"
      :hero-stats="heroStats"
      :featured-game="featuredGame"
      :floating-games="floatingGames"
      :current-dot="currentDot"
      @explore-games="exploreGames"
      @watch-trailer="watchTrailer"
      @set-featured-game="setFeaturedGame"
      @switch-hero-content="switchHeroContent"
      :get-particle-style="getParticleStyle"
      :get-floating-game-style="getFloatingGameStyle"
    />

    <Products :games="games" />

    <About />

    <Footer />
  </div>
</template>

<script>
// Kode script (data, methods, dll.) di App.vue tetap sama seperti sebelumnya
// ... (semua kode script Anda dari sebelumnya ada di sini)
// ...
// ...
import Navbar from './components/navbar.vue';
import Carousel from './components/carousel.vue';
import Products from './components/products.vue';
import About from './components/about.vue';
import Footer from './components/footer.vue';
import './assets/main.css';

export default {
  name: 'App',
  components: {
    Navbar,
    Carousel,
    Products,
    About,
    Footer
  },
  data() {
    return {
      isMenuOpen: false,
      welcomeVisible: false,
      statsVisible: false,
      gameShowcaseActive: false,
      scrollIndicatorVisible: false,
      shapeAnimations: false,
      typedText: '',
      typeIndex: 0,
      typeTexts: ['Epic Adventure', 'Thrilling Experience', 'Gaming Journey'],
      currentTypeText: 0,
      cursorBlink: true,
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
        { id: 1, title: "Cyber Knights 2024", genre: "Action RPG", rating: "⭐⭐⭐⭐⭐", price: "49.99", icon: "🤖" },
        { id: 2, title: "Forest Quest", genre: "Adventure", rating: "⭐⭐⭐⭐⭐", price: "29.99", icon: "🌲" },
        { id: 3, title: "Space Odyssey", genre: "Sci-Fi", rating: "⭐⭐⭐⭐⭐", price: "39.99", icon: "🚀" },
        { id: 4, title: "Dragon's Realm", genre: "Fantasy", rating: "⭐⭐⭐⭐⭐", price: "59.99", icon: "🐉" },
        { id: 5, title: "Racing Thunder", genre: "Racing", rating: "⭐⭐⭐⭐⭐", price: "34.99", icon: "🏎️" },
        { id: 6, title: "Mystery Island", genre: "Puzzle", rating: "⭐⭐⭐⭐⭐", price: "24.99", icon: "🏝️" }
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
          setTimeout(() => { this.eraseText(); }, 2000);
        }
      };
      const eraseText = () => {
        if (this.typedText.length > 0) {
          this.typedText = this.typedText.slice(0, -1);
          setTimeout(eraseText, 50);
        } else {
          this.currentTypeText = (this.currentTypeText + 1) % this.typeTexts.length;
          this.typeIndex = 0;
          setTimeout(typeText, 500);
        }
      };
      this.eraseText = eraseText;
      typeText();
      setInterval(() => { this.cursorBlink = !this.cursorBlink; }, 500);
    },
    switchHeroContent(index) {
      this.currentDot = index;
      this.currentGradient = this.gradients[index];
      this.setFeaturedGame(this.floatingGames[index % this.floatingGames.length]);
    },
    exploreGames() {
      document.getElementById('games').scrollIntoView({ behavior: 'smooth' });
    },
    watchTrailer() {
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
      const angles = [0, 60, 120, 180, 240, 300];
      const radius = 120;
      const angle = angles[index] * Math.PI / 180;
      return {
        transform: `translate(${Math.cos(angle) * radius}px, ${Math.sin(angle) * radius}px)`,
        animationDelay: index * 0.2 + 's'
      };
    }
  }
}

</script>