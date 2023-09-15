<script setup>
    import {ref} from 'vue'
    import Tabla from './Tabla.vue'

    let articulo=ref('')
    let cantidad=ref(1)
    let valorU=ref(1)

    

    function agregar(){

        if(articulo.value.trim()!=='' && cantidad.value>0 && valorU.value>0){
            articulos.value.push({nombre:articulo.value, cantidad:cantidad.value, valorU:valorU.value})
            articulo.value=''
            cantidad.value=1
            valorU.value=1
        }
    }
    function eliminar(posicion){
        articulos.value.splice(posicion,1)
    }

    let articulos=ref([])
</script>



<template>
     <section class="form-section">
            
            <form class="form" action="">
                <h1>Formulario</h1>
                <div>
                    <label>Articulo</label>
                    <input v-model="articulo" class="input" type="text">
                </div>
    
                <div>
                    <label>Cantidad</label>
                    <input v-model="cantidad" class="input" type="number">
                </div>
                <div>
                    <label>Valor unitario</label>
                    <input v-model="valorU" class="input" type="number">
    
                </div>
                <button type="button" @click="agregar">Agregar</button>
    
            </form>

    </section>

    <section class="table-section">
        <Tabla :articulos="articulos" @eliminar="eliminar"></Tabla>
    </section>
        
       
  
</template>


<style scoped>
    

    .form-section{
        background-color: rgb(206, 206, 206);
        display: flex;
        justify-content: center;
        align-items: center;
    }
    
    .form{
        display: grid;
        grid-template-rows: 1fr 1fr 1fr 1fr;
        gap: 20px;
    }

    .form .input{
        width: 300px;
        margin-left: 10px;
    }

    .form button{
        width: 100px
    }
</style>