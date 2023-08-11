<template>
	<div class="countdown-container">
		<span id="countdown-number">{{ this.timer.seconds }}</span>
        <svg>
            <circle r="32" cx="34" cy="34" :class="{ run: this.timer.run }"></circle>
        </svg>
	</div>
</template>

<script>
export default {
	name: "Countdown",
    props: {
        init: {
            type: Boolean
        },
        seconds: {
            type: Number,
            default: 60
        }
    },
    watch: { 
        init: function () {
            this.initCountdown(); 
        }
    },
	emits: ["countdown-over"],
    data() {
        return {
            timeout: 0,
            timer: {
                seconds: 60,
                run: false
            }
        }
    },
    watch: {
        timer: function (obj) {
            debugger;
        }
    },
    methods: {
        initCountdown() {
            this.timer.seconds = this.seconds;
            this.timer.run = true;
            this.timeout = setInterval(() => {
                if (this.timer.seconds === 0) {
                    this.stopCountdown();
                    this.$emit("countdown-over", true);
                }
                this.timer.seconds--;
            }, 1000);
        },

        stopCountdown() {
            this.timer.run = false;
            this.timer.seconds = this.seconds;
            clearInterval(this.tiemout);
        }
    },
    mounted() {
        this.initCountdown();
    }
};
</script>

<style scoped>
#countdown-container {
    position: relative;
    margin: auto;
    margin-top: 100px;
    height: 40px;
    width: 40px;
    text-align: center;
}
#countdown-number {
    color: var(--main-color);
    font-weight: bolder;
    font-size: 35px;
}
svg {
    position: absolute;
    width: 69px;
    height: 69px;
    transform: rotateY(-180deg) rotateZ(-90deg);
}
svg circle {
    stroke: var(--main-color);
    stroke-dasharray: 198px;
    stroke-dashoffset: 0px;
    stroke-linecap: round;
    stroke-width: 5px;
    fill: none;
}
svg circle.run {
    animation: countdown v-bind(seconds/1.7 + 's') linear forwards;
}

@keyframes countdown {
    from {
        stroke-dashoffset: 0px;
    }
    to {
        stroke-dashoffset: 113px;
    }
}
</style>
