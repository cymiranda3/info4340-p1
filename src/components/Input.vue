<template>
    <div>
        <input required id='input' type='date' v-if='displayInput' v-model="date">
        <button id='button' v-if='displayInputButton' v-on:click="getDate">set date</button>
        <p v-if='displayInputMessage'>please input a future date...</p>

    </div>
</template>
<script type='js'>
// Import moment.js package
import moment from 'moment';

export default {
  data() {
    return {
      date: '',
      displayInput: true,
      displayInputButton: true,
      displayReset: false,
      displayInputMessage: true,
    };
  },
  mounted() {
    this.$options.interval = setInterval(this.checkInputDisp, 10);
  },
  methods: {
    getDate() {
        const date = this.date;
        // Storing the date
        if (typeof(Storage) !== 'undefined') {
            localStorage.setItem('date', date);
            this.displayInput = true;
            this.displayInputButton = true;
        }
        this.displayInput = false;
        this.displayInputButton = false;
        this.displayReset = true;
    },
    checkInputDisp() {
      const now = moment();
      const input = moment(this.date);
      if (localStorage.getItem('date') === null && input.diff(now, 'days') >= 0) {
        this.displayInput = true;
        this.displayInputButton = true;
        this.displayInputMessage = false;
      } else if (localStorage.getItem('date') === null && input.diff(now, 'days') < 0) {
        this.displayInput = true;
        this.displayInputButton = false;
        this.displayInputMessage = true;
      }
    },
  },
};
</script>

<style>
  input[type='date'] {
    margin-right: 1vw;
    background-color: transparent;
    border: none;
    border-bottom: 3px solid white;
    color: white;
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    font-size: 20px;
  }

  button {
    padding: 10px;
    background-color: transparent;
    border: 1px solid white;
    border-radius: 3px;
    color: white;
    margin-top: 10px;
  }

  p {
    color: white;
  }

  @media only screen and (max-width: 600px) {
    input[type='date'] {
      display: block;
      margin-left: 25vw;
      margin-right: 25vw;
      width: 40vw;
      padding-left: 0px;
    }
    button {
      display: block;
      margin: 0 auto;
    }
  }
</style>
