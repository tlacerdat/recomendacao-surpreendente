<template>
  <div class="container-countdown">
    <div class="base-timer">
      <svg
        class="base-timer__svg"
        viewBox="0 0 100 100"
        xmlns="http://www.w3.org/2000/svg"
      >
        <g class="base-timer__circle">
          <circle class="base-timer__path-elapsed" cx="50" cy="50" r="45" />
          <path
            :stroke-dasharray="circleDasharray"
            class="base-timer__path-remaining"
            :class="!displayBlueRing ? 'd-none' : ''"
            d="
            M 50, 50
            m -45, 0
            a 45,45 0 1,0 90,0
            a 45,45 0 1,0 -90,0
          "
          ></path>
        </g>
      </svg>

      <div class="base-timer__text">
        <h3>Vamos conectar você em:</h3>
        <span class="base-timer__label">
          {{ formattedTimeLeft }}
        </span>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    // in seconds
    duration: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      timerInterval: null,
      timePassed: 0,
      displayBlueRing: true,
      call: [{ id: '39jdjk', id_meet: 'ums-hufo-qgw', default: true }],
    }
  },
  computed: {
    formattedTimeLeft() {
      const timeLeft = this.timeLeft
      let minutes = Math.floor(timeLeft / 60)
      let seconds = timeLeft % 60

      if (this.timeLeft < 1) {
        this.displayBlueRingFunc()
        this.redirectUser()
        return '00:00'
      }
      if (seconds < 10) {
        seconds = `0${seconds}`
      }

      if (minutes < 10) {
        minutes = `0${minutes}`
      }

      return `${minutes}:${seconds}`
    },
    timeLeft() {
      return this.duration - this.timePassed
    },
    circleDasharray() {
      let x = 283 - (this.timeFraction * 283).toFixed(0)
      if (x < 0) {
        x = 0
      }
      return `${x} 283`
    },
    timeFraction() {
      const rawTimeFraction = (this.timePassed + 0.05) / this.duration
      return rawTimeFraction
    },
  },
  mounted() {
    this.startTimer()
  },
  methods: {
    startTimer() {
      this.timerInterval = setInterval(() => {
        if (this.duration <= this.timePassed) {
          clearInterval(this.timerInterval)
          return
        }
        this.timePassed += 1
      }, 1000)
    },
    displayBlueRingFunc() {
      setTimeout(() => {
        this.displayBlueRing = false
      }, 1000)
    },
    redirectUser() {
      setTimeout(() => {
        const callId = this.getUrlParameter('call')
        let searchedItem
        if (callId && callId.length > 0) {
          searchedItem = this.call.find((element) => element.id === callId)
        }

        if (searchedItem) {
          window.location.href =
            'https://meet.google.com/' + searchedItem.id_meet
        } else if (!searchedItem && callId.length > 0) {
          window.location.href =
            'https://meet.google.com/' +
            this.call.find((element) => element.default === true).id_meet
        } else {
          window.location.reload()
        }
      }, 1500)
    },
    getUrlParameter(name) {
      // eslint-disable-next-line no-useless-escape
      name = name.replace(/[\[]/, '\\[').replace(/[\]]/, '\\]')
      const regex = new RegExp('[\\?&]' + name + '=([^&#]*)')
      const results = regex.exec(location.search)
      return results === null
        ? ''
        : decodeURIComponent(results[1].replace(/\+/g, ' '))
    },
  },
}
</script>
<style scoped lang="scss">
.container-countdown {
  max-width: 65%;
  margin: 1rem auto;
}
/* Sets the containers height and width */
.base-timer {
  position: relative;
  width: 100%;
  height: 100%;
  /* Removes SVG styling that would hide the time label */
  &__circle {
    fill: none;
    stroke: none;
  }
  /* The SVG path that displays the timer's progress */
  &__path-elapsed {
    stroke-width: 0.2rem;
    stroke: rgba($color: #fff, $alpha: 0.16);
  }

  &__text {
    font-family: $fontb;
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;

    h3 {
      font-size: 1.7rem;
      margin-bottom: 0;
    }

    span {
      font-size: 7.75rem;
      line-height: 0.95;
    }
  }

  &__path-remaining {
    /* Just as thick as the original ring */
    stroke-width: 0.2rem;
    /* Rounds the line endings to create a seamless circle */
    stroke-linecap: round;
    /* Makes sure the animation starts at the top of the circle */
    transform: rotate(90deg);
    transform-origin: center;
    /* One second aligns with the speed of the countdown timer */
    transition: 1s linear all;
    /* Allows the ring to change color when the color value updates */
    stroke: $blue;
  }
  &__svg {
    // /* Flips the svg and makes the animation to move left-to-right
    transform: scaleX(-1);
  }
}

@media only screen and (max-width: 767px) {
  .container-countdown {
    max-width: 95%;
    margin: 2rem 0 2.5rem auto;
  }

  .base-timer {
    &__text {
      h3 {
        font-size: 1rem;
      }

      span {
        font-size: 4.375rem;
      }
    }
  }
}
</style>
