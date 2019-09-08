<template>
    <div>
        <button id='button' v-if='displayReset' v-on:click="resetDate">reset countdown</button>
    </div>
</template>

<script type='js'>
export default {
  data() {
    return {
      date: '',
      displayReset: true,
    };
  },
  mounted() {
    this.$options.interval = setInterval(this.checkResetDisp, 10);
  },
  methods: {
    resetDate() {
      localStorage.removeItem('date');
    },
    checkResetDisp() {
      if (localStorage.getItem('date') === null) {
        this.displayReset = false;
      } else {
        this.displayReset = true;
      }
    },
  },
};
</script>

<style>
  input[type='date'] {
    padding: 10px;
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
</style>