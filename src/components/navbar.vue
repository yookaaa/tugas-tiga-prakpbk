<template>
  <nav class="navbar">
    <div class="nav-container">
      <div class="nav-logo">
        <h2>🎮 yookaaStore</h2>
      </div>
      <ul class="nav-menu" :class="{ active: isMenuOpen }" id="nav-menu">
        <li class="nav-item">
          <a href="#home" class="nav-link" @click="$emit('close-menu')">Home</a>
        </li>
        <li class="nav-item">
          <a href="#games" class="nav-link" @click="$emit('close-menu')">Games</a>
        </li>
        <li class="nav-item">
          <a href="#about" class="nav-link" @click="$emit('close-menu')">About</a>
        </li>
        <li class="nav-item">
          <a href="#contact" class="nav-link" @click="$emit('close-menu')">Contact</a>
        </li>
      </ul>
      <div class="nav-toggle" @click="$emit('toggle-menu')" :aria-expanded="isMenuOpen ? 'true' : 'false'" aria-controls="nav-menu">
        <span class="bar"></span>
        <span class="bar"></span>
        <span class="bar"></span>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
  // Menerima data 'isMenuOpen' dari induk
  props: ['isMenuOpen']
}
</script>