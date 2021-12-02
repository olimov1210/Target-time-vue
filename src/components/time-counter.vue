<template>
  <div class="time-counter">
    <div>
      <h1 class="target-time-remaining">TARGET TIME REMAINING</h1>
      <div class="active-cases-section"><h2>{{activeCases}}</h2><p>POSITIVES TODAY</p></div>
    </div>
    <div class="time-counter-main">
      <!-- months section -->
      <vue-ellipse-progress
          :data="circles"
          :progress="monthsProgress"
          :angle="-90"
          color="#D93E0D"
          :size="140"
          :thickness="6"
          emptyThickness="0%"
          line="round"
          :legend="true"
          :legendValue="monthValue"
          dash="50 0.8"
          animation="rs 600 200"
          :noData="false"
          :loading="false"
          fontColor="white"
          :half="false"
          fontSize="4rem">
        <p class="type-of-time" slot="legend-caption">months</p>
      </vue-ellipse-progress>
      <!-- end of months section -->
      <!-- days section -->
      <vue-ellipse-progress
          :data="circles"
          :progress="daysProgress"
          :angle="-90"
          color="#D93E0D"
          :size="140"
          :thickness="6"
          emptyThickness="0%"
          line="round"
          :legend="true"
          :legendValue="daysValue"
          dash="50 0.8"
          animation="rs 600 200"
          :noData="false"
          :loading="false"
          fontColor="white"
          :half="false"
          fontSize="4rem">
        <p class="type-of-time" slot="legend-caption">days</p>
      </vue-ellipse-progress>
      <!-- end of days section -->
      <!-- hours section -->
      <vue-ellipse-progress
          :data="circles"
          :progress="hoursProgress"
          :angle="-90"
          color="#D93E0D"
          :size="140"
          :thickness="6"
          emptyThickness="0%"
          line="round"
          :legend="true"
          :legendValue="hoursValue"
          dash="50 0.8"
          animation="rs 600 200"
          :noData="false"
          :loading="false"
          fontColor="white"
          :half="false"
          fontSize="4rem">
        <p class="type-of-time" slot="legend-caption">hours</p>
      </vue-ellipse-progress>
      <!-- end of hours section -->
      <!-- minutes section -->
      <vue-ellipse-progress
          :data="circles"
          :progress="minutesProgress"
          :angle="-90"
          color="#D93E0D"
          :size="140"
          :thickness="6"
          emptyThickness="0%"
          line="round"
          :legend="true"
          :legendValue="minutesValue"
          dash="50 0.8"
          animation="rs 600 200"
          :noData="false"
          :loading="false"
          fontColor="white"
          :half="false"
          fontSize="4rem">
        <p class="type-of-time" slot="legend-caption">minutes</p>
      </vue-ellipse-progress>
      <!-- end of minutes section -->
      <!-- seconds section -->
      <vue-ellipse-progress
          :data="circles"
          :progress="secondsProgress"
          :angle="-90"
          color="#D93E0D"
          :size="140"
          :thickness="6"
          emptyThickness="0%"
          line="round"
          :legend="true"
          :legendValue="secondsLegend"
          dash="50 0.8"
          animation="rs 600 200"
          type="loop"
          :noData="false"
          :loading="false"
          fontColor="white"
          :half="false"
          fontSize="4rem">
          <span slot="legend-value" class="legend-value">.{{millisecondsValue}}</span>
        <p class="type-of-time" slot="legend-caption">seconds</p>
      </vue-ellipse-progress>
      <!-- end of seconds section -->
      <!-- milliseconds section -->
      <!-- end of seconds section -->

    </div>
    <p class="targeted-time">to 31 Dec 2021</p>
  </div>
</template>.
// script section
<script>

export default {
  name: "timeCounter",
  props: {
    activeCases: {
      type: Number,
      required: true
    },
  },
  data() {
    return {
      circles: [],
      monthsProgress: 0,
      monthValue: 0,
      daysProgress: 0,
      daysValue: 0,
      hoursProgress: 0,
      hoursValue: 0,
      minutesProgress: 0,
      minutesValue: 0,
      secondsProgress: 0,
      secondsLegend: 0,
      millisecondsValue: 0,
    }
  },
  mounted() {
    this.setTimer();
  },
  methods: {
    getDaysOfMonth(date) {
      const year = date.getFullYear()
      const months = date.getMonth()
      return new Date(year, months + 1, 0).getDate();
    },
    setTimer() {
      this.sTimer = setInterval(()=>{
        const date = new Date();
        const daysOfMonth = this.getDaysOfMonth(date);
        this.monthsProgress = (11 - date.getMonth()) * 100 / 11
        this.monthValue = 11 - date.getMonth()
        this.daysProgress = (daysOfMonth - date.getDate()) * 100 / daysOfMonth
        this.daysValue = daysOfMonth - date.getDate()
        this.hoursProgress = (24 - date.getHours()) * 100 /24
        this.hoursValue = 24 - date.getHours()
        this.minutesProgress = (60 - date.getMinutes()) * 100 / 60
        this.minutesValue = 60 - date.getMinutes()
      }, 1000)
      this.msTimer = setInterval(()=>{
        const date = new Date();
        this.secondsProgress = (60 - date.getSeconds()) * 100 /60
        this.secondsLegend = 60 - date.getSeconds();
        this.millisecondsValue = (100 - date.getMilliseconds() / 10).toString().charAt(0);
      }, 100)
    },
  },
  destroyed: function(){
    clearInterval(this.sTimer)
    clearInterval(this.msTimer)
  },
}
</script>
// end of script section
// style section
<style scoped>
.time-counter {
  font-family: 'Roboto Condensed', sans-serif;
  background: linear-gradient(90deg, #6a0000, #010156);
  width: 1000px;
  padding: 1px 30px 1px 30px;
  margin-left: 140px;
  color: white;
}
.time-counter-main {
  display: flex;
  justify-content: space-between;
}
.ep-container{
  margin-left: -10px;
  background: rgba(0,0,0,.2);
  border-radius: 50%;
}
.target-time-remaining {
  text-align: center;
  margin-bottom: 0px;
  font-size: 45px;
  margin-top: 13px;
}
.targeted-time {
  text-align: center;
  color: rgba(255, 255, 255, .6);
}
.type-of-time {
  margin-top: -5px;
  margin-bottom: 0px;
  font-size: 14px;
}
.active-cases-section {
  display: flex;
  justify-content: center;
  margin-bottom: 40px;
  margin-top: 10px;
}
.active-cases-section h2 {
  font-size: 45px;
  margin: 0px;
}
.active-cases-section p {
  font-size: 20px;
  font-weight: normal;
  margin-left: 8px;
}
.legend-value {
  font-size: 2rem;
}
</style>
// end of style section