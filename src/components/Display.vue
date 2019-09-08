<template>
  <div>
      <div id="dayCountdown" v-show='dispComp' v-text="days"></div>
      <h2 id='subheader' v-show='dispComp'>days left!</h2>
  </div>
</template>

<script>
import moment from 'moment';

export default {
  data() {
    return {
      days: 999,
      dispComp: false,
    };
  },
  mounted() {
    this.$options.interval = setInterval(this.updateDays, 10);
  },
  beforeDestroy() {
    clearInterval(this.$options.interval);
  },
  methods: {
    updateDays() {
      if (localStorage.getItem('date') !== null) {
        const now = moment();
        const dateInput = moment(localStorage.getItem('date'));
        this.days = dateInput.diff(now, 'days') + 1;
        this.dispComp = true;
      } else {
        this.dispComp = false;
      }
    },
  },
};
</script>

<style>
  #dayCountdown {
    font-size: 5vw;
    color: white;
  }

  #subheader {
    color: white;
    font-size: 3vw;
    margin-top: 0px;
  }

  @media only screen and (max-width: 600px) {
      #dayCountdown {
        font-size: 10vw;
      }
    }
</style>
