<script setup> 
/* const props = defineProps(['title', 'id' , 'body' , 'colortext']) 
console.log(props.title)
console.log(props.id)
console.log(props.body)
*/
const props = defineProps({
    title: String,
    id: Number,
    body:{
        type:String,
        default: "Sin descripcion"
    },
   // cambiarFavorito: Function,
})
const emin = defineEmits(['cambiarFavoritoNombre'])
//emin('cambiarFavoritoNombre',title)
//console.log(props.id)
</script>
<template>
    <div class="card">
        <div class="card-body">
            <h5 class="card-title" :class="`text-${colortext}`">{{ title }} - {{ id }}</h5>
            <p>{{ body }}</p>
                <button @click="emin('cambiarFavoritoNombre',title)" class="btn btn-outline-success">Favorito</button>  
         <!---  <button @click="cambiarFavorito(title)" class="btn btn-outline-success">Favorito</button> -->
        </div>

    </div>
    
</template>