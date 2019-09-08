<template>
  <div id="app">
    <h1 id="greeting">Hi, Barb!</h1>
    <Input />
    <Display />
    <Reset />
  </div>
</template>

<script lang="js">
import { Component, Vue } from 'vue-property-decorator';
import HelloWorld from './components/HelloWorld.vue';
import Input from './components/Input.vue';
import Display from './components/Display.vue';
import Reset from './components/Reset.vue';
import moment from 'moment';


@Component({
  components: {
    HelloWorld,
    Input,
    Display,
    Reset,
  },
})

export default class App extends Vue {
  data() {
    return {
      displayInputComponent: true,
      displayDisplayComponent: false,
      stor: localStorage.getItem('date'),
    };
  }
  mounted() {
    if (localStorage.getItem('date') === null) {
      this.displayDisplayComponent = false;
      this.displayInputComponent = true;
    } else {
      this.displayDisplayComponent = true;
      this.displayInputComponent = false;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

html {
  background-image: linear-gradient(pink, blue);
  height: 100vh;
}

#greeting {
  font-size: 10vw;
  color: white;
  margin-bottom: 0px;
}
</style>
