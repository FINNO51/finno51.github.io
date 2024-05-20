<script setup>
defineProps({
  msg: {
    type: String,
    required: true,
  },
});
</script>

<template>
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <h3>
      Ingeniero del Software, desarrollador.<br />
      <a
        href="https://www.linkedin.com/in/jordi-conde-molina/"
        target="_blank"
        rel="noopener"
        >Linkedin</a
      >
      -
      <a href="https://github.com/FINNO51" target="_blank" rel="noopener"
        >GitHub</a
      >
    </h3>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    text-align: left;
  }
}
</style>
