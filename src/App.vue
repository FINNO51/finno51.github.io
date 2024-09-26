<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import TheWelcome from "./components/TheWelcome.vue";
import WeatherWidget from "./components/WeatherWidget.vue";
</script>

<template>
  <header>
    <div class="wrapper">
      <img
        alt="Logo"
        class="logo"
        src="./assets/logo.png"
        width="125"
        height="125"
      />
      <HelloWorld msg="Jordi Conde Molina" />
      <WeatherWidget />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

main {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
