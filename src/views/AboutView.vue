<template>
  <div class="about">
    <h1>This is an about page</h1>

    <p> {{ texto }}</p>
    <p> {{ despedida }}</p>
    <input type="text" v-bind:value="contenidoTexto"> <br>
    <button v-on:click="despedirse">Ver despedida</button>
    
  </div>
</template>

<script>
export default {
  name: 'About component',
  data: function(){
    return{
    texto: 'esto es un texto',
    despedida: ' ',
    contenidoTexto: 'contenido del modelo',
    }
  },
  methods: {
  despedirse: function(){
    this.despedida ="me voy mañana"
  }
 }
}

</script>
