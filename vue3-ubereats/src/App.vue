<template>
	<div id="app"></div>
	<Home />
</template>

<script>
import Home from "./pages/home.vue";
export default {
	name: "App",
	components: {
		Home,
	},
};
</script>

<style lang="scss">
@import url("./style/reset.css");
@import url("https://fonts.googleapis.com/css2?family=Roboto%3Awght%40300%3B400%3B700&display=swap");
#app {
	font-family: "Roboto", sans-serif;
	padding: 0 20px;
}
</style>
