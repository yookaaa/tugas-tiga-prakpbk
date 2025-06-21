<template>
  <section id="games" class="featured-games">
    <div class="container">
      <h2 class="section-title">Featured Games</h2>
      <div class="games-grid">
        <div class="game-card" v-for="game in games" :key="game.id">
          <div class="card-image">
            <div class="game-thumbnail">{{ game.icon }}</div>
            <div class="card-overlay">
              <button class="play-btn">Play Now</button>
            </div>
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
</template>

<script>
export default {
  props: ['games']
}
</script>