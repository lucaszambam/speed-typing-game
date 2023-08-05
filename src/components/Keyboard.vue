<template>
	<div class="keyboard-container">
		<div class="keys-container">
			<div class="key-cap" v-for="key in this.keys" :data-key="key">{{ key }}</div>
		</div>
	</div>
</template>

<script>
export default {
	name: "Keyboard",
	emits: ["key-pressed"],
	methods: {
		registerKeyEventListener() {
			document.addEventListener("keyup", (event) => {
				$(`.key-cap[data-key="${event.key}"]`).removeClass("pressed");
			});

			document.addEventListener("keydown", (event) => {
				this.$emit("key-pressed", event.key);
				$(`.key-cap[data-key="${event.key}"]`).addClass("pressed");
			});
		},
	},
	mounted() {
		this.registerKeyEventListener();
	},
	data() {
		return {
			keys: ["q", "w", "e", "r", "t", "y", "u", "i", "o", "p",
				   "a", "s", "d", "f", "g", "h", "j", "k", "l",
				   "z", "x", "c", "v", "b", "n", "m", ",", "."]
		};
	},
};
</script>

<style scoped>
.keys-container {
	display: flex;
	flex-wrap: wrap;
	max-width: 600px;
	gap: 0.9rem;
	justify-content: center;
}

.key-cap {
	font-weight: bolder;
	border: 2px solid var(--border-color);
	color: var(--main-color);
	border-radius: 0.4rem;
	width: 40px;
	height: 40px;
	display: flex;
	justify-content: center;
	align-items: center;
	user-select: none;
	transition: all 0.15s;
}

.key-cap.pressed {
	background-color: rgba(var(--main-color-rgb) / 0.4);
	scale: 1.2;
}
</style>
