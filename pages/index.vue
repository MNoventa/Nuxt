<template lang="html">
  <div class="container"> <!-- elemento raiz, no puedo tener varios divs hermanos -->
    <h1 class="title">Albums</h1>
    <div class="columns is-multiline">
      <!-- :album="album" es la propiedad que especificamos en el prop del componente -->
      <AlbumCard :album="album" v-for="album in albums" />      
    </div>
  </div>
</template>
<script>
  import AlbumCard from '../components/albumcard';
  export default {
    name: 'IndexPage',

    components: {
      AlbumCard
    },

    //cualquier propiedad que retornamos desde el metodo data, lo podemos usar como variable en la vista
    data(){
      return{
        // mensaje: '',
        // albums: []
      }
    },

    async asyncData ({ $axios, params, error }) {
      return await $axios.get(`${process.env.endpoint}/albums`)
      .then((res) => {
        return {
          albums: res.data,
        }
      })
      .catch((e) => {
        error({ statusCode: 404, message: 'Post not found' })
      })
    }
  }
</script>

<style>
  body{
    margin-top: 50px;
  }
</style>
