<template>
	<div id="app">
		<div class="central-area">
			<TextContainer />
			<Keyboard @key-pressed="keyPress" />
		</div>
	</div>
</template>

<script>
import TextContainer from "./components/TextContainer.vue"; 
import Keyboard from "./components/Keyboard.vue";

export default {
	name: "App",
	components: {
		Keyboard,
		TextContainer
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
.central-area {
	max-width: 50%;
	display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
	gap: 4rem;
}
</style>
