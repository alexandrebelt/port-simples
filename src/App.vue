<template>
  <HelloWorld />
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import HelloWorld from './components/HelloWorld.vue';
import LocomotiveScroll from 'locomotive-scroll';

export default defineComponent({
  name: 'App',
  components: {
    HelloWorld
  },
  mounted(){
    const locomotiveScroll = new LocomotiveScroll()
  }
});
</script>

<style lang="scss">
@font-face {
  font-family: 'Cotford Var', serif;
  src: url('./assets/fonts/CotfordVar/CotfordVar.ttf') format('truetype');
}

@font-face {
  font-family: 'Neue Haas Grotesk Display';
  src: url('./assets/fonts/NeueHaasGrotesk/NeueHaasGroteskDisplay-Thin.otf') format('opentype');
  font-weight: 100;
}

@font-face {
  font-family: 'Neue Haas Grotesk Display';
  src: url('./assets/fonts/NeueHaasGrotesk/NeueHaasGroteskDisplay-ExtLt.otf') format('opentype');
  font-weight: 200
}

@font-face {
  font-family: 'Neue Haas Grotesk Display';
  src: url('./assets/fonts/NeueHaasGrotesk/NeueHaasGroteskDisplay-Light.otf') format('opentype');
  font-weight: 300;
}

@font-face {
  font-family: 'Neue Haas Grotesk Display';
  src: url('./assets/fonts/NeueHaasGrotesk/NeueHaasGroteskDisplay-SemLt.otf') format('opentype');
  font-weight: 400;
}

@font-face {
  font-family: 'Neue Haas Grotesk Display';
  src: url('./assets/fonts/NeueHaasGrotesk/NeueHaasGroteskDisplay-Reg.otf') format('opentype');
  font-weight: 500;
}

@font-face {
  font-family: 'Neue Haas Grotesk Display';
  src: url('./assets/fonts/NeueHaasGrotesk/NeueHaasGroteskDisplay-Medium.otf') format('opentype');
  font-weight: 600;
}

@font-face {
  font-family: 'Neue Haas Grotesk Display';
  src: url('./assets/fonts/NeueHaasGrotesk/NeueHaasGroteskDisplay-Bold.otf') format('opentype');
  font-weight: 700;
}

@font-face {
  font-family: 'Neue Haas Grotesk Display';
  src: url('./assets/fonts/NeueHaasGrotesk/NeueHaasGroteskDisplay-Black.otf') format('opentype');
  font-weight: 800;
}

:root {
  --cotford: 'Cotford Var', serif;
  --neue: 'Neue Haas Grotesk Display', sans-serif;
}

* {
  margin: 0;
  padding: 0;
}

body {
  background-color: #242424;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #FFF;
  font-family: var(--neue);
}

.container {
  padding: 50px 30px;
}

.limit {
  max-width: 900px;
  margin: 0 auto;
}

h1,
h4 {
  font-family: var(--cotford) !important;
  font-weight: 100;
}

h1 {
  text-align: center;
}

h4 {
  font-size: 24px;
}

p {
  font-size: 15px;
}

a {
  text-decoration: none !important;

}
</style>
