<template>
	<div id="app">
		<div class="central-area">
			<TextContainer :typed-letter="this.keyPressed"/>
			<Keyboard @key-pressed="keyPress" />
		</div>
	</div>
</template>

<script>
import TextContainer from "./components/TextContainer.vue"; 
import Keyboard from "./components/Keyboard.vue";

export default {
	name: "App",
	data() {
		return {
			keyPressed: '',
			keyIndex: 0,
		}
	},
	components: {
		Keyboard,
		TextContainer
	},
	methods: {
		keyPress(key) {
			this.keyPressed = {
				id: this.keyIndex + 1,
				value: key
			};
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
