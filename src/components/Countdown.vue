<template>
	<div class="countdown-container">
        <div class="base-timer">
            <svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
                <g class="base-timer-circle">
                <circle class="base-timer-path-elapsed" cx="50" cy="50" r="45"></circle>
                <path stroke-dasharray="279" class="base-timer-path-remaining" d=" M 50, 50 m -45, 0 a 45,45 0 1,0 90,0 a 45,45 0 1,0 -90,0"></path>
                </g>
            </svg>
            <span id="base-timer-label" class="base-timer-label">{{ this.timer.seconds }}</span>
        </div>
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
            },
            fullDashArray: 279
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
                
                this.setCircleDasharray();
                this.timer.seconds--;
            }, 1000);
        },

        stopCountdown() {
            this.timer.run = false;
            this.timer.seconds = this.seconds;
            clearInterval(this.tiemout);
        },

        setCircleDasharray() {
            const circleDasharray = `${(this.fullDashArray * this.timer.seconds / this.seconds).toFixed(0)} ${this.fullDashArray}`;
            $(".base-timer-path-remaining").attr("stroke-dasharray", circleDasharray);
        }
    },
    mounted() {
        this.initCountdown();
    }
};
</script>

<style scoped>
.base-timer {
  position: relative;
  width: 140px;
  height: 140px;
}
.base-timer-circle {
  fill: none;
  stroke: none;
}

.base-timer-path-elapsed {
  stroke-width: 7px;
  stroke: grey;
}

.base-timer-path-remaining {
  stroke-width: 7px;
  stroke-linecap: round;
  transform: rotate(90deg);
  transform-origin: center;
  transition: 1s linear all;
  fill-rule: nonzero;
  stroke: currentColor;
  color: var(--main-color);
}
.base-timer-label {
  position: absolute;
  width: 140px;
  height: 140px;
  top: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 45px;
  font-family: monospace;
}
</style>
