<template>
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
            <tr v-for="(articulo,index) of props.articulos" :key="index">
                <td >{{ index+1}}</td>
                <td >{{ articulo.nombre}}</td>
                <td >{{ articulo.cantidad}}</td>
                <td >{{ articulo.valorU}}</td>
                <td >{{ articulo.cantidad*articulo.valorU}}</td>
                <td><button @click="eliminar(index)">Eliminar</button></td>
                
            </tr>

        </tbody>

    </table>
    <h3>Total compra: {{ calcTotalC }}</h3>
    <h3>Descuento: {{ calcDesc }}%</h3>
</template>


<script setup> 


    


    
    import {ref, defineProps,defineEmits,computed} from 'vue'


    const props=defineProps({
        articulos:Object
    
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

        let descuento=0

        if(calcTotalC.value>=60000 && calcTotalC.value<120000){
            descuento=5
        }else if(calcTotalC.value>=120000 && calcTotalC.value<240000){
            descuento=10
        }else if (calcTotalC.value>=240000){
            descuento=15
        }

        return descuento
    })




    



</script>


<style scoped>
    .table{
        width: 500px;
    }
</style>