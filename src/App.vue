<template>
	<div id="app">
		<div class="top-area">
			<Countdown :init="this.keyIndex > 0"/>
		</div>

		<div class="central-area">
			<TextContainer :typed-letter="this.keyPressed"/>
			<Keyboard @key-pressed="keyPress" />
		</div>

		<div class="bottom-area">
			<GameStatus :started="this.keyIndex > 0" @restart="restartGame"/>
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
import GameStatus from "./components/GameStatus.vue";

export default {
	name: "App",
	data() {
		return {
			keyPressed: '',
			keyIndex: 0,
			startGame: false,
		}
	},
	components: {
    Countdown,
    Keyboard,
    TextContainer,
    GameStatus
},
	methods: {
		keyPress(key) {
			this.keyPressed = {
				id: this.keyIndex++,
				value: key
			};
		},

		restartGame() {
			this.startGame = true;
		}
	}
};
</script>

<style>
#app {
	font-family: "Cutive Mono", Helvetica, Arial, sans-serif;
	color: white;
	font-size: 25px;
	display: flex;
	justify-content: center;
	align-items: center;
	height: 98vh;
	width: 99vw;   
	display: flex;
    flex-direction: column;
	gap: 4rem;
}
.central-area {
	max-width: 50%;
	display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
	gap: 4rem;
}
.bottom-area {
	margin-top: 100px;
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
