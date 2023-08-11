<template>
	<div id="app">
		<div class="timer-area">
			<Countdown :init="true"/>
		</div>

		<div class="central-area">
			<TextContainer :typed-letter="this.keyPressed"/>
			<Keyboard @key-pressed="keyPress" />
		</div>

		<div class="github-repo">
			<a href="https://github.com/lucaszambam/speed-typing-game" target="_blank">
				<img src = "./assets/svg/github-mark-white.svg" alt="GitHub Repository"/>
			</a>
		</div>
	</div>
</template>

<script>
import Countdown from "./components/Countdown.vue"; 
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
		Countdown,
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
	display: flex;
    flex-direction: column;
}
.central-area {
	max-width: 50%;
	display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
	gap: 4rem;
}
.github-repo {
	position: fixed;
    bottom: 10px;
    right: 20px;
}
.github-repo a img {
	scale: 0.45;
    opacity: 0.5;
	transition: all .25s;
}
.github-repo a img:hover {
	opacity: 1;
	scale: 0.5;
}
</style>
