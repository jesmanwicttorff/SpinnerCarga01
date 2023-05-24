<!----<script>
i
  components: { BlogPost },mport { ref } from "vue"
export default{
    setup() {
    const counter = ref(0);
    const increment = () => {
      counter.value ++;
    }
    return {
      counter,
      increment
    }
},
}
</script>
<template>
  <h1>Hola Mundo</h1><br/>
  <button @click="increment">{{ counter }}</button>
</template>
-->
<script setup>
import BlogPost from "./components/BlogPost.vue";
import ButtonCounter from "./components/ButtonCounter.vue"
import { ref , computed, onMounted} from "vue"
import PaginatePost from "./components/PaginatePost.vue"
import LoadingSpinner from "./components/LoadingSpinner.vue"
import LoadingSpinnerVue from "./components/LoadingSpinner.vue";
const favorito = ref('') // lo definimos reactivo
const PosXpage = 10
const inicio = ref(0)
const fin = ref(PosXpage)
 
const MaxLength = computed(() => post.value.length); 

const cambiarFavorito = (title) =>{
  favorito.value = title
}
const post = ref([]);

 /* const post = ref([
  {id :'1', title:'Post 1', body:'Descripcion 1'},
  {id :'2', title:'Post 2', body:'Descripcion 2'},
  {id :'3', title:'Post 3', body:'Descripcion 3'},
  {id :'4', title:'Post 4'}
]);
*/
const next = () => {
 inicio.value = inicio.value + PosXpage
 fin.value = fin.value + PosXpage
}

const prev = () =>{
   inicio.value = inicio.value -  PosXpage 
   fin.value =  fin.value -  PosXpage 
}
const loading = ref(true)

onMounted(() => 
{
  fechData()
})
    const fechData = async()=>{
            try {
          const res = await fetch('https://jsonplaceholder.typicode.com/posts')
          post.value = await res.json() // await nos devuelve la promesa
        } catch(e){
          console.log(e)
        } finally {
          setTimeout(()=>{ // el setTimeout se va ejecutar este call back despues de 2
            loading.value =false},2000)}
          
    }
   // fechData()
 /* fetch('https://jsonplaceholder.typicode.com/posts')
  .then(res => res.json())
  .then(data=> post.value = data)
  .catch((e)=>console.log(e))
  .finally(()=>{
  setTimeout(()=>{ // el setTiemout se va ejecutar este call back despues de 2 seg 
    loading.value = false},2000)})
    */

</script>
<template>
  <LoadingSpinner v-if="loading"/>
  <div class="containe" v-else>
    <h1>Hola Mundo  {{ favorito }}</h1><br>
      <ButtonCounter/><br/><br>
     <!---- <ButtonCounter class="mb-2"/><br/>-->
      <PaginatePost class="mb-2" 
          @next="next" 
          @prev="prev" 
          :inicio="inicio" 
          :fin="fin"
          :tamaño="MaxLength"

          /> 
      <blog-post v-for="poste in post.slice(inicio,fin)"
          :key = "poste.id"  
          :id =poste.id
          :title="poste.title"
          :body="poste.body"
          @cambiarFavoritoNombre="cambiarFavorito"
          >
        </blog-post>
        
        <!--  :cambiarFavorito="cambiarFavorito"--> 
    <!----  <blog-post id = "2" title="Post 2" body="Descripcion 2" colortext="danger"/> -->
    <!----  <blog-post id = "3" title="Post 3"  colortext="success"/> -->
  </div>
  
</template>