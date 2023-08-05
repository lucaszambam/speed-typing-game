<template>
	<div class="text-container">
		<span>{{ this.text }}</span>
	</div>
</template>

<script>
import texts from "/src/assets/texts/texts.json";

export default {
	name: "TextContainer",
    data() {
        return {
            text: ''
        }
    },
	methods: {
		getText() {
            try {
                return texts[(Math.floor(Math.random() * texts.length))].text;
            } catch(err) {
                console.error('[texts.json not found...]');
                console.error(err);
            }
        }
	},
    beforeMount() {
        this.text = this.getText();
    }
};
</script>

<style scoped>
.text-container {
    display: flex;
    max-height: 130px;
    overflow: hidden;
    font-size: 30px;
    font-weight: 500;
}
</style>
