<template>

    <div class="table-container">
        <table class="table">
        <thead>
            <tr>
                <th>#</th>
                <th>Articulo</th>
                <th>Cantidad</th>
                <th>V.Unitario</th>
                <th>Total</th>
                <th>Eliminar</th>
            </tr>
        </thead>

        <tbody>
            <tr v-for="(articulo,posicion) of props.articulos" :key="posicion">
                <td >{{ posicion+1}}</td>
                <td >{{ articulo.nombre}}</td>
                <td >{{ articulo.cantidad}}</td>
                <td >{{ articulo.valorU}}</td>
                <td >{{ articulo.cantidad*articulo.valorU}}</td>
                <td><button @click="eliminar(posicion)">Eliminar</button></td>
                
            </tr>

        </tbody>

    </table>

    </div>

    <div class="text-container">
        <h3>Total compra: {{ calcTotalC.toLocaleString('es-CO', {
            style: 'currency',
            currency: 'COP'
        }) }}</h3>
        <h3>Descuento: ({{ calcDesc }}%) {{ calcTotalC*(calcDesc/100) }}</h3>
        <h3>Total a pagar: {{ calcPagar.toLocaleString('es-CO', {
            style: 'currency',
            currency: 'COP'
        }) }}</h3>

    </div>
    
</template>


<script setup> 

    
    import {ref, defineProps,defineEmits,computed} from 'vue'


    const props=defineProps({
        articulos:Array
    
    })

    let posicion=ref(0)

    const emit=defineEmits(['eliminar'])

    function eliminar(index){
        emit('eliminar',index)
    }

    const calcTotalC=computed(()=>{

        let totalC=0

        props.articulos.forEach(articulo => {

            totalC+=articulo.cantidad*articulo.valorU
            
        });
        

        return totalC
    })
    
   



    const calcDesc=computed(()=>{

        let descuentoPrecio=0

        let descuentoCantidad=0

        let descuento=0

        // Descuento por precio
        if(calcTotalC.value>=60000 && calcTotalC.value<120000){
            descuentoPrecio=5
        }else if(calcTotalC.value>=120000 && calcTotalC.value<240000){
            descuentoPrecio=10
        }else if (calcTotalC.value>=240000){
            descuentoPrecio=15
        }

        // Descuento por cantidad
        if(props.articulos.length>=6 && props.articulos.length<12){
            descuentoCantidad=10
        }else if(props.articulos.length>=12){
            descuentoCantidad=20
        }

        descuento=Math.max(descuentoPrecio,descuentoCantidad)

        return descuento
    })

    const calcPagar=computed(()=>{return calcTotalC.value*(1-calcDesc.value/100)})




    



</script>


<style scoped>

    .text-container{
        margin-left: 20px;
    }

    .table-container{
        width: 100%;
        height: 500px;
        max-height:  500px;
        overflow: auto;
        margin-bottom: 20px;
    }
    .table {
        border-collapse: collapse;
        width: 100%;
        height: 100%;
    }

    th {
        background-color: #f2f2f2;
        text-align: left;
        padding: 20px;
        border-bottom: 1px solid #ddd;
    }

    td {
        padding: 5px;
        border-bottom: 1px solid #ddd;
        text-align: center;
    }

   

</style>