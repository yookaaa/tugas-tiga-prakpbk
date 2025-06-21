<template>
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
          Yuk, jelajahi dunia penuh kemungkinan seru! Dari petualangan seru sampai teka-teki yang bikin mikir, temukan game favoritmu di koleksi premium pilihan kami.
        </p>
        <div class="hero-stats">
          <div class="stat-card" v-for="(stat, index) in heroStats" :key="index" :class="{ visible: statsVisible }" :style="{ animationDelay: index * 0.2 + 's' }">
            <div class="stat-icon">{{ stat.icon }}</div>
            <div class="stat-info">
              <div class="stat-number">{{ stat.number }}</div>
              <div class="stat-label">{{ stat.label }}</div>
            </div>
          </div>
        </div>
        <div class="hero-actions">
          <button class="cta-btn primary" @click="$emit('explore-games')">
            <span class="btn-text">Explore Games</span>
            <span class="btn-icon">🚀</span>
          </button>
          <button class="cta-btn secondary" @click="$emit('watch-trailer')">
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
            <div class="game-icon-float" v-for="(game, index) in floatingGames" :key="index" :style="getFloatingGameStyle(index)" @click="$emit('set-featured-game', game)">
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
      <div class="nav-dot" v-for="n in 3" :key="n" :class="{ active: currentDot === n - 1 }" @click="$emit('switch-hero-content', n - 1)"></div>
    </div>
  </section>
</template>

<script>
export default {
  props: [
    'currentGradient',
    'shapeAnimations',
    'welcomeVisible',
    'statsVisible',
    'gameShowcaseActive',
    'scrollIndicatorVisible',
    'typedText',
    'cursorBlink',
    'heroStats',
    'featuredGame',
    'floatingGames',
    'currentDot',
    'getParticleStyle',
    'getFloatingGameStyle'
  ]
}
</script>