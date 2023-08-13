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
            type: Boolean,
            default: false
        },
        seconds: {
            type: Number,
            default: 60
        }
    },
    watch: { 
        init: function (doInit) {
            if (doInit) {
                this.initCountdown();
            }
        }
    },
	emits: ["countdown-over"],
    data() {
        return {
            timer: {
                seconds: 60,
            },
            fullDashArray: 279
        }
    },
    methods: {
        initCountdown() {
            this.timer.seconds = this.seconds;
            this.timeout = setInterval(() => {
                
                if (this.timer.seconds === 0) {
                    this.stopCountdown();
                    this.$emit("countdown-over", true);
                } else {
                    this.timer.seconds--;
                    this.setCircleDasharray();
                }
                
            }, 1000);
        },

        stopCountdown() {
            clearInterval(this.timeout);
            $(".base-timer-path-remaining").attr("stroke-dasharray", "0 999");
        },

        restartCountdown() {
            this.timer.seconds = this.seconds;
            $(".base-timer-path-remaining").attr("stroke-dasharray", this.fullDashArray);
            this.initCountdown();
        },

        setCircleDasharray() {
            const circleDasharray = `${(this.fullDashArray * this.timer.seconds / this.seconds).toFixed(0)} ${this.fullDashArray}`;
            $(".base-timer-path-remaining").attr("stroke-dasharray", circleDasharray);
        }
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
  color: var(--color-pass);
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
