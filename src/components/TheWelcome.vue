<script setup>
import WelcomeItem from "./WelcomeItem.vue";
import ShipIcon from "./icons/IconShip.vue";
import BombIcon from "./icons/IconBomb.vue";
import BananaIcon from "./icons/IconBanana.vue";
import { ref, reactive } from "vue";

const video = ref(true);

function toggleVideo() {
  video.value = !video.value;
}
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
        <BananaIcon />
      </template>
      <template #heading
        ><a
          href="https://github.com/Pablo01bm/fanana"
          target="_blank"
          rel="noopener"
          >Fanana</a
        ></template
      >

      Aplicación Android destinada tanto a profesorado como alumnado de colegios
      para personas con discapacidad. Realizada por un equipo de seis personas
      usando metodología SCRUM y programada en
      <a href="https://flutter.dev/" target="_blank" rel="noopener">Flutter</a>,
      yo me dediqué principalmente al Front-End. Me siento particularmente
      orgulloso del login usando pictogramas para personas con discapacidad
      motora e intelectual, el cual conseguí sacar adelante rápidamente en un
      alarde de inspiración.
      <a @click="toggleVideo()" :style="{ cursor: 'pointer' }"
        >Aquí se puede ver una pequeña demo</a
      >.
    </WelcomeItem>
    <Transition>
      <div
        v-show="video"
        :style="{ 'padding-left': '5em', 'padding-right': '5em' }"
        class="video"
      >
        <iframe
          src="https://drive.google.com/file/d/1ZXvs5m_txfGJhsDG55yebWUk7dkfM11s/preview"
          width="100%"
          height="250vw"
          allow="autoplay"
        ></iframe>
      </div>
    </Transition>
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

<style scoped>
.video {
  margin-top: 2rem;
  display: flex;
  position: relative;
}

@media (min-width: 1024px) {
  .video {
    margin-top: 0;
    padding: 0.4rem 0 1rem calc(var(--section-gap) / 2);
  }

  .video:before {
    content: " ";
    border-left: 1px solid var(--color-border);
    position: absolute;
    left: 0;
    bottom: calc(50% + 0px);
    height: calc(50% - 0px);
  }

  .video:after {
    content: " ";
    border-left: 1px solid var(--color-border);
    position: absolute;
    left: 0;
    top: calc(50% + 0px);
    height: calc(50% - 0px);
  }

  .video:first-of-type:before {
    display: none;
  }

  .video:last-of-type:after {
    display: none;
  }
}
</style>
