<template>
  <div class="count-down">
    <div class="timer-grid">
      <div class="timer">
        <div class="datetime">{{ displayDays }}</div>
        <span>days</span>
      </div>
      <div class="timer">
        <div class="datetime">{{ displayHours }}</div>
        <span>hours</span>
      </div>
      <div class="timer">
        <div class="datetime">{{ displayMinutes }}</div>
        <span>minutes</span>
      </div>
      <div class="timer">
        <div class="datetime">{{ displaySeconds }}</div>
        <span>seconds</span>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      displaySeconds: 0,
      displayMinutes: 0,
      displayHours: 0,
      displayDays: 0
    }
  },
  computed: {
    _seconds: () => 1000,
    _minutes() {
      return this._seconds * 60
    },
    _hours() {
      return this._minutes * 60
    },
    _days() {
      return this._hours * 24
    }
  },
  mounted() {
    this.showRemaining()
  },
  methods: {
    showRemaining() {
      const timer = setInterval(() => {
        const now = new Date();
        const end = new Date(2023, 11, 23, 59, 59, 59);

        const distance = end.getTime() - now.getTime();

        if (distance < 1) {
          clearInterval(timer)
          return
        }

        const days = Math.floor(distance / this._days)
        const hours = Math.floor((distance % this._days) / this._hours)
        const minutes = Math.floor((distance % this._hours) / this._minutes)
        const seconds = Math.floor((distance % this._minutes) / this._seconds)

        this.displayDays = days < 10 ? "0" + days : days;
        this.displayHours = hours < 10 ? "0" + hours : hours;
        this.displayMinutes = minutes < 10 ? "0" + minutes : minutes;
        this.displaySeconds = seconds < 10 ? "0" + seconds : seconds;

      }, 1000)
    }
  }
}
</script>
<style>
.timer-grid {
  display: grid;
  grid-template-columns: 50px 50px 50px 50px;
  column-gap: 15px;
  position: absolute;
  top: 50%;
  transform: translateY(-100%);
}

.count-down {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.timer {
  width: 90px;
  height: 120px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
  flex-shrink: 0;
}

.timer .datetime {
  flex: 2;
  font-size: 3rem;
  text-align: center;
  padding-top: 15px;
}

.timer span {
  display: block;
  flex: 1;
  font-size: 1.2rem;
  text-align: center;
  padding-top: 7px;
}
</style>