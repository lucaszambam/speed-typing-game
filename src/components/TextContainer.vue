<template>
	<div class="text-container">
        <span v-for="word in this.words" class="word">
		    <span v-for="letter in word.letters" class="letter" :class="{ current: letter.current }">
                {{ letter.value }}
            </span>
        </span>
	</div>
</template>

<script>
import texts from "/src/assets/texts/texts.json";

export default {
	name: "TextContainer",
    props: ["typed-letter"],
    watch: { 
        typedLetter: (newVal, oldVal) => {
            console.log('Prop changed: ', newVal, ' | was: ', oldVal)
        }
    },
    data() {
        return {
            current: '',
            words: [],
            letters: [],
            letter: {
                current: false,
                typed: false,
                value: ''
            }
        }
    },
	methods: {
		initText() {
            try {
                const text = texts[Math.floor(Math.random() * texts.length)].text;
                const words = text.match(/\S+|\s+/g);

                this.words = words.map((word, indexWord) => {
                    const lettersObject = word.split('').map((letter, indexLetter) => ({
                        current: (indexWord === 0 && indexLetter === 0),
                        typed: false,
                        value: letter
                    }));
                    return {letters: lettersObject};
                });
            } catch(err) {
                console.error('[could not read texts.json...]');
                console.error(err);
            }
        }
	},
    beforeMount() {
        this.initText();
    }
};
</script>

<style scoped>
.text-container {
    display: flex;
    flex-wrap: wrap;
    max-height: 130px;
    overflow: hidden;
    font-size: 30px;
    font-weight: 500;
}
.word {
    display: flex;
}
.letter {
    width: 16px;
}
.letter.current {
    color: var(--main-color);
}
</style>
