<template>
	<div class="text-container">
        <span v-for="word in this.words" class="word">
		    <span v-for="letter in word.letters" class="letter" :class="{ current: letter.current, miss: letter.miss, pass: letter.pass }">
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
        typedLetter: function (letterInput) {
            this.updateText(letterInput.value); 
        }
    },
    data() {
        return {
            words: [],
            availableWords: [],
            misses: 0,
            wordsTyped: 0,
        }
    },
	methods: {
		initText() {
            try {
                const text = texts[Math.floor(Math.random() * texts.length)].text;
                const words = text.match(/\S+|\s+/g);

                this.words = words.map((word, indexWord) => {
                    const lettersObject = word.split('').map((letter, indexLetter) => ({
                        id: indexLetter,
                        current: (indexWord === 0 && indexLetter === 0),
                        miss: null,
                        pass: null,
                        value: letter
                    }));

                    return {
                        id: indexWord,
                        letters: lettersObject
                    };
                });
                this.availableWords = JSON.parse(JSON.stringify(this.words));
            } catch(err) {
                console.error('[could not read texts.json...]');
                console.error(err);
            }
        },
        updateText(letterInput) {
            const currentWord = {...this.availableWords[0]};
            const currentLetter = {...currentWord.letters[0]};

            if (currentLetter.value === letterInput) {
                this.words[currentWord.id].letters[currentLetter.id].pass = true;
            } else {
                this.words[currentWord.id].letters[currentLetter.id].miss = true;
                this.misses++;
            }

            this.words[currentWord.id].letters[currentLetter.id].current = false;
            this.availableWords[0].letters.shift(0);

            if (currentWord.letters.length === 0) {
                this.wordsTyped++;
                this.words[currentWord.id + 1].letters[0].current = true;
                this.availableWords.shift(0);
            } else {
                this.words[currentWord.id].letters[currentLetter.id + 1].current =  true;
            }
        }
	},
    beforeMount() {
        this.initText();
    },
    mounted() {
        setInterval(() => {
            $('.letter.current').toggleClass('pipe');
        }, 500)
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
    gap: 0.2rem;
}
.letter {
    width: 16px;
}
.letter.current {
    position: relative;
}
.letter.current.pipe::before {
    content: '|';
    position: absolute;
    left: -10px;
}
.letter.miss {
    color: red;
}
.letter.pass {
    color: green;
}
</style>
