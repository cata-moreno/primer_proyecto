<template>
    <div id="Juegos">
       
    <div class="contenedorPadre">

        <div v-for="(juego,index) in juegos" v-bind:key="index" class="card m-2" style="width: 18rem;">
                        <img v-bind:src="juego.background_image" class="card-img-top" alt="logo">
                        <div class="card-body">
                            <h5 class="card-title">{{juego.name}}</h5>
                            <p class="card-text">ESRB Rating: {{  juego.esrb_rating.name }}</p>
                        </div>
                        <ul class="list-group list-group-flush">
                            <li class="list-group-item">Rating: {{ juego.rating }}</li>
                            <li class="list-group-item">Released: {{  juego.released }}</li>
                            <li class="list-group-item">Updated: {{  juego.updated }}</li>
                        </ul>
                        <div class="card-body">
                            <a v-on:click="mostrarOpiniones(juego.name)" class="btn btn-primary">Opinar</a><br>
                            <br><a v-on:click="irAdministracion(juego.name)" class="btn btn-danger ">Like</a>
                            
                        </div>
                </div>

    </div>

    </div>
</template>

<script>
    import axios from 'axios';

    export default{
        name: 'Juegos',
        data:function(){
            return{
            cantidadJuegos:0,
            juegos:[],
            }
        },
        methods:{
            consumirApi:function(){

                let url='https://api.rawg.io/api/games?key=8eb1b64aeb1c4e10832e21f9b87eb4a3';               
                    axios(url)
                        .then(respuesta =>{
                            console.log(respuesta);
                            
                            this.cantidadJuegos = respuesta.data.results.length;
                            for(let i=0; i < this.cantidadJuegos; i++){
                            this.juegos.push(respuesta.data.results[i]);
                        }
                    })

                        .catch(error =>{
                            console.log(error);
                        });
            },
            mostrarOpiniones:function(nombreJuego){
                this.$router.push(`/opiniones/${nombreJuego}`);
            },
            irAdministracion:function(nombreJuego){
                this.$router.push(`/administracion/${nombreJuego}`);
            },
        },
        created(){
            this.consumirApi();
        }      
    }
</script>

<style scooped>
    #Juegos{
        background-color: #F0FFF0;
        
    }

    .contenedorPadre{
        display:flex;
        flex-wrap: wrap;
        justify-content: center;
        padding: 4%;
        
    }
</style>