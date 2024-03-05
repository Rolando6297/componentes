<script setup>
import BlogPost from './components/BlogPost.vue';
import ButtonC from './components/ButtonCounter.vue';
import PaginatePost from './components/PaginatePost.vue'
import LoadingSpinner from './LoadingSpinner.vue';
import { computed, onMounted, ref } from 'vue';
const post =ref([]);
const favorito = ref("ninguno");
const postXpage = 10;
const inicio = ref(0);
const fin = ref(postXpage);
const loading =ref(true);
const cambiarFav = (parametro) => { 
 
    favorito.value = parametro;
 }
onMounted(async()=>{
  loading.value=true;
  try {
    const res = await fetch("https://jsonplaceholder.typicode.com/posts")
    post.value = await res.json()
  } catch (error) {
    console.log(error)
  }finally{
    loading.value=false
  }
})
//fetch("https://jsonplaceholder.typicode.com/posts").then(res=> res.json()).then(data => {
  //  post.value = data;
//}).finally(()=> loading.value=false)


const nextPage = () =>{
  inicio.value = inicio.value + postXpage;
  fin.value = fin.value + postXpage;
}
const prevPage = () =>{
  inicio.value = inicio.value - postXpage;
  fin.value = fin.value - postXpage;
}
const maxLength = computed (()=> post.value.length);
</script>

<template>
  <LoadingSpinner v-if="loading"></LoadingSpinner>
  <div class="container text-center mt-3" v-else>
    <h1>Componentes</h1>
    <h2>My Favorite post: {{ favorito }}</h2>
    <br>

    <PaginatePost class="mb-2"  
    @nextPage="nextPage" 
    @prevPage="prevPage"
    :inicio="inicio"
    :fin=" fin"
    :longitud = "maxLength"
    
    ></PaginatePost>


    <BlogPost v-for="elemento in post.slice(inicio,fin)" 
    :key="elemento.id" 
    :title="elemento.title" 
    :id="elemento.id" 
    :body="elemento.body" 
    :color="elemento.color"
    @cambiarFavEmit="cambiarFav"
    class="mb-2"
    />
   
    <BlogPost title="Post 03" :id="3" @cambiarFavEmit="cambiarFav" color="danger"/> <!--no se manda props description y se pone por default en el objeto-->
  </div>
</template>

<style >

</style>
