<template>
  <div
    v-bind:style="{
      marginLeft: '10vw',
      marginRight: '10vw',
    }"
  >
    <div
      class="data-container"
      v-for="value in newArray"
      v-bind:key="value - Math.random() * Math.random()"
    >
      <div
        v-bind:style="{
          height: value + 'px',
          width: this.barWidth + 'vw',
          marginLeft: this.barMargin + 'px',
          fontSize: this.barFont + 'px',
        }"
        v-bind:class="{
          'array-element': true,
          active_wrong: wrong === value,
          active_right: right === value,
        }"
      >
        {{ value }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  props: ["newArray", "wrong", "right"],
  data() {
    return {
      barWidth: 3,
      barMargin: 1,
      barFont: 5,
    };
  },

  watch: {
    immediate: true,
    deep: true,
    newArray(newArray) {
      // watch it if array change
      this.barWidth = 60 / newArray.length;
      this.barMargin = 1;
      this.barFont = 100 / newArray.length;
    },
  },
};
</script>

<style scoped>
.data-container {
  width: 100%;
  height: 100%;
  background-color: rgb(230, 230, 230);
  text-align: center;
}
.array-element {
  background: #6299f1;
  position: relative;
  /* left: 5%; */
  float: left;
}
.active_wrong {
  background-color: lightcoral;
  transform: scaleX(1.2);
}
.active_right {
  background-color: lightgreen;
  transform: scaleX(1.2);
}
</style>
