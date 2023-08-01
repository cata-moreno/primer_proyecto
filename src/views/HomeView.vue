<template>
  <div class="home">
    <h2>Juegos Disponibles</h2>
    <Juegos></Juegos>
  </div>
</template>

<script>
// @ is an alias to /src

import Juegos from '@/components/Juegos.vue';

export default {
  name: 'HomeView',
  components: {
    Juegos
  }
}
</script>
