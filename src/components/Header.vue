<template>
  <div class="Header">
    <div><button v-on:click="generate">Create new array</button></div>
    <div class="slider">
      <h4>Change array size</h4>
      <vue-slider v-model="value" v-bind="options" @change="generateArray" />
      <h4>Change sorting speed</h4>
      <vue-slider v-model="speed" v-bind="options" @change="changeSpeed" />
    </div>
    <div class="algorithms">
      <button v-on:click="selection">selection sort</button>
      <button v-on:click="bubble">Bubble sort</button>
    </div>
  </div>
  <Home
    v-bind:newArray="newArray"
    v-bind:wrong="wrongElement"
    v-bind:right="rightElement"
  />
</template>

<script>
import Home from "./Home";
import VueSlider from "vue-slider-component";
import "vue-slider-component/theme/antd.css";
// delay function
const delay = (ms) => new Promise((res) => setTimeout(res, ms));

export default {
  name: "Header",
  components: { VueSlider, Home },
  //  data like useState
  data() {
    return {
      newArray: [...Array(20)].map(() => ~~(Math.random() * 540)),
      value: 20,
      speed: 30,
      options: { min: 5, max: 100, height: 10 }, // slider options
      wrongElement: undefined,
      rightElement: undefined,
    };
  },
  methods: {
    // array generate function
    generateArray: function() {
      this.newArray = [...Array(this.value)].map(
        () => ~~(Math.random() * Math.random() * 940)
      );
    },
    //change array speed
    changeSpeed: function() {
      this.speed = this.value;
    },
    // Selection sort algo
    selection: async function() {
      let start = this.newArray;
      for (let i = 0; i < this.newArray.length; i++) {
        let min = i;
        await delay(this.speed * 10);
        for (let j = i + 1; j < this.newArray.length; j++) {
          if (start != this.newArray) {
            return;
          }
          if (this.newArray[j] < this.newArray[min]) {
            min = j;
          }
        }
        let temp = this.newArray[min];
        this.rightElement = temp;
        this.wrongElement = this.newArray[i];
        this.newArray[min] = this.newArray[i];
        this.newArray[i] = temp;
      }
    },
    // bubble sort algo
    bubble: async function() {
      let start = this.newArray;
      for (let i = 0; i < this.newArray.length; i++) {
        for (let j = 0; j < this.newArray.length - i + 1; j++) {
          await delay(100);
          if (start != this.newArray) {
            return;
          }
          if (this.newArray[j] > this.newArray[j + 1]) {
            let temp = this.newArray[j + 1];
            this.rightElement = temp;
            this.wrongElement = this.newArray[j];
            this.newArray[j + 1] = this.newArray[j];
            this.newArray[j] = temp;
          }
        }
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.Header {
  height: 25vh;
  background-color: darkgray;
  display: flex;
  align-items: center;
  justify-content: space-evenly;
}
.algorithms {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-evenly;
}
button {
  border: none;
  outline: none;
  background-color: darkgray;
  color: black;
  font-size: 1rem;
  font-weight: bold;
}
button:hover {
  transform: scale(1.2);
  cursor: pointer;
}
.slider {
  color: black;
  font-size: 1rem;
  font-weight: bold;
}
</style>
