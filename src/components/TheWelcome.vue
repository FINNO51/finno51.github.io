<script setup>
import WelcomeItem from "./WelcomeItem.vue";
import ShipIcon from "./icons/IconShip.vue";
import BombIcon from "./icons/IconBomb.vue";
</script>

<template>
  <div>
    <WelcomeItem>
      <template #icon>
        <BombIcon />
      </template>
      <template #heading
        ><a target="_self" href="https://finno51.github.io/MineSweeper/"
          >MineSweeper</a
        ></template
      >

      Proyecto de experimentación con
      <a href="https://vuejs.org/" target="_blank" rel="noopener">Vue.js</a>.
      Realizado en un fin de semana como reto para ver hasta qué punto se podía
      conseguir una aplicación funcional. Con diseño web responsive y
      personalización de las partidas.
    </WelcomeItem>

    <WelcomeItem>
      <template #icon>
        <ShipIcon />
      </template>
      <template #heading
        ><a target="_self" href="https://finno51.github.io/SG_SistemasGraficos/"
          >F-Alpha</a
        ></template
      >

      Proyecto de informática gráfica con JavaScript haciendo uso de
      <a href="https://threejs.org/" target="_blank" rel="noopener">Three.js</a
      >, desarrollado en colaboración con
      <a href="https://github.com/Pablo01bm" target="_blank" rel="noopener"
        >Pablo Borrego Megías</a
      >. Aunque originalmente fuese un simple trabajo de universidad, pronto
      tomó mayor envergadura.
    </WelcomeItem>
  </div>
</template>
