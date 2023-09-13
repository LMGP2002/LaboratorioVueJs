<script setup>
    import {ref} from 'vue'
    import Tabla from './Tabla.vue'

    let articulo=ref('')
    let cantidad=ref(0)
    let valorU=ref(0)

    

    function agregar(){
        articulos.value.push({nombre:articulo.value, cantidad:cantidad.value, valorU:valorU})
    }
    function eliminar(posicion){
        articulos.value.splice(posicion,1)
    }

    let articulos=ref([])
</script>



<template>
    <main class="main">
        <section class="form-container">
            
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
        
        <section>
            <Tabla :articulos="articulos" @eliminar="eliminar"></Tabla>
        </section>
      
        </main>
</template>


<style scoped>
    .main{
        display: flex;
        gap: 200px;
       
    }
    .form-container{
        width: 500px;
        height: 600px;
        background-color: rgb(206, 206, 206);
        display: flex;
        padding: 20px;
        justify-content: center;
        align-items: center;
    }
    
    .form{
        
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 50px;

    }

    .form .input{
        width: 300px;
        margin-left: 10px;
    }

    .form button{
        width: 100px
    }
</style>