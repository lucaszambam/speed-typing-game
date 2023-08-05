<template>
	<div id="app">
		<Keyboard @key-pressed="keyPress" />
	</div>
</template>

<script>
import Keyboard from "./components/Keyboard.vue";
// import TextArea from "./components/TextArea.vue";

export default {
	name: "App",
	components: {
		Keyboard,
	},
	methods: {
		keyPress(key) {
			console.log(key);
		}
	}
};
</script>

<style>
#app {
	font-family: "Cutive Mono", Avenir, Helvetica, Arial, sans-serif;
	color: white;
	font-size: 25px;
	display: flex;
	justify-content: center;
	align-items: center;
	height: 98vh;
	width: 99vw;
}
</style>
