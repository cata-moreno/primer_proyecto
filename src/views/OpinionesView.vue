<template>
    <div id="OpinionesView">
        <h1>Opiniones</h1>
        <p>Escribe tu opnión para el juego: {{ nombre }}</p>
        <hr>

        <div class="container" id="divForm">
            <form>
                <div class="mb-3">
                    <label for="txtNombre" class="form-label">Nombre:</label>
                    <input type="text" class="form-control" id="txtNombre" v-model="nombreEnviado" aria-describedby="txtNombreHelp">
                    <div id="txtNombreHelp" class="form-text">Ingrese su nombre</div>
                </div>
                <div class="mb-3">
                    <label for="txtOpinion" class="form-label">Opinión:</label>
                    <input type="text" class="form-control" id="txtOpinion" v-model="opinionEnviada">
                </div>
                <button type="submit" v-on:click.prevent="agregarOpinion()" class="btn btn-info">{{nombreBoton}}</button>
            </form>
        </div>
        <hr>

        <h3>A continuación podrás ver tu opnión</h3>
        <div id="sinOpiniones"  v-if="cantidadOpiniones<1">
            <p>No existen opiniones para mostrar</p>
        </div>
        <hr>

        <div class="accordion" id="accordionExample" v-if="cantidadOpiniones>0">
            <div class="accordion-item" v-for="(elemento,index) in opiniones">
                <h2 class="accordion-header">
                <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#collapseOne" aria-expanded="true" aria-controls="collapseOne">
                    Opinion creada por: {{ elemento.nombre }}
                </button>
                </h2>
                <div id="collapseOne" class="accordion-collapse collapse show" data-bs-parent="#accordionExample">
                    <div class="accordion-body">
                        {{ elemento.opinion }}
                    </div>
                    <button class="btn btn-danger" v-on:click="eliminarOpinion(index)">Eliminar</button><br>
                    <br><button class="btn btn-warning" v-on:click="editarOpinion(index)">Editar</button>
                </div>

            </div>

        </div>

    <hr>
  
        <router-link to="/">Volver</router-link>

    </div>
</template>

<script>
export default{
    name:'OpinionesView',
    props:['nombre'],
    data: function(){
        return{
            cantidadOpiniones: 0,
            nombreEnviado:'',
            opinionEnviada:'',
            opiniones:[],
            nombreBoton:'Agregar',
            indiceActualizar:0,

        }
    },
    methods:{
        agregarOpinion: function(){

        if(this.nombreBoton == 'Agregar'){
            this.cantidadOpiniones++;
            let nuevaOpinion={
            nombre:this.nombreEnviado,
            opinion:this.opinionEnviada,
                            };
            this.opiniones.push(nuevaOpinion);
            this.nombreEnviado='';
            this.opinionEnviada='';
        }
        else if(this.nombreBoton=='Actualizar'){
            let opinionActualizada={
                nombre:this.nombreEnviado,
                opinion:this.opinionEnviada,
                            };
            this.opiniones.splice(this.indiceActualizar,1, opinionActualizada);
            alert('La opinión fue actualizada. Revise el apartado con la nueva información');
        }},

        eliminarOpinion:function(indice){
        this.cantidadOpiniones--;
        this.opiniones.splice(indice,1);
        },
        editarOpinion:function(indice){
        this.nombreEnviado=this.opiniones[indice].nombre;
        this.opinionEnviada=this.opiniones[indice].opinion;
        this.nombreBoton = 'Actualizar';
        this.indiceActualizar = indice;
        alert('Va a editar una opinión. Revise el formulario con la información cargada');
        },
        }
    }
        
</script>

<style scooped>
#OpinionesView{
    background-color: #F0FFF0;
}
#divForm{
    text-align:left;
}
#sinOpiniones{
    border: 2px solid red;
    margin-left: 10%;
    margin-right:10%;
}
</style>