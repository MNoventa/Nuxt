<template lang="html">
	<div class="box column is-one-quarter">
		<h3>Title: {{album.title}}</h3>
		<nuxt-link :to="'/albums/' + album.id" class="button is-primary">Ver álbum</nuxt-link>
	</div>
</template>

<script>
	export default{
		name: 'AlbumCard',
		// props: objeto json en el que definimos propiedades en el que otros componentes se pueden comunicar con ellos con las etiquetas
		props:{
			album: Object
		}
	}

</script>

<style scoped>
	.box{
		margin: 1em;
	}
	h3{
		min-height: 4.5em;
	}
</style>