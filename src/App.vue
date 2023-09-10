<script setup lang="ts">
import background from './assets/background.png'
import Header from './components/Header.vue'
import Main from './components/Main.vue'
</script>

<template>
  <div :style="{ backgroundImage: `url(${background})` }"
    class="bg-[#040f20] bg-no-repeat bg-cover bg-center w-[3840px] h-[1080px] font-sans text-white">
    <Header></Header>
    <Main></Main>
    <footer></footer>
  </div>
</template>11520 3240

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
