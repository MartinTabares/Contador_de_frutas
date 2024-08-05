<template>
	<div id="app">
		<NavBar />
		<Products />
	</div>
</template>

<script>
import NavBar from './components/NavBar.vue'
import Products from './components/Products.vue';
// import MainView from './components/MainView.vue'

export default {
	name: 'App',
	components: {
		NavBar,
		Products
	}
}
</script>
