<template lang="html">
	<div class="container">
		<h1 v-text class="title">Album</h1>
		<div class="box">
		  <h3 v-text="album.title"></h3>
		  <img :src="photos.url" loading="lazy" class=""/>
		  <nuxt-link to="/" class="button is-primary">Inicio</nuxt-link>
	  </div>
  </div>
</template>

<script>
	// npm install vue-router
	import router from 'vue-router';

	export default{
		name: 'AlbumIndvPage',

		data(){
			return{
				album: {},
				photos: []
			}
		},

		created(){
			console.log(this.$route);
			let albumId = this.$route.params.id;
		},

		async asyncData ({ $axios, route, params, error }) {
      let album = await $axios.get(`${process.env.endpoint}/albums/${params.id}`)
      .then((res) => {
        return res.data;
      })
      .catch((e) => {
        error({ statusCode: 404, message: 'Error 404 OMG lol' })
      })

      let photos = await $axios.get(`${process.env.endpoint}/photos/${params.id}`)
      .then((res) => {
        return res.data;
      })
      .catch((e) => {
        error({ statusCode: 404, message: 'Error 404 OMG lol' })
      })

      return {
      	album,
      	photos
      }
	  }
	}
</script>

<style>
	img{
		width: 100%;
		margin: auto;
		display: block;
		height: 100px;
		margin-bottom: 25px;
	}

	.box{
		width: 400px;
		margin-top: 50px;
	}

	a{
		margin: auto;
	}

	body{
		margin-top: 50px;
	}
	
	h3{
		margin-bottom: 25px;
	}
</style>