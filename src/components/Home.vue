<template>
  <div
    class="data-container"
    v-for="value in newArray"
    v-bind:key="value - Math.random() * Math.random()"
  >
    <div
      class="array-element"
      v-bind:style="{
        height: value + 'px',
        width: this.barWidth + 'px',
        marginLeft: this.barMargin + 'px',
        fontSize: this.barFont + 'px',
      }"
    >
      {{ value }}
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  props: ["newArray"],
  data() {
    return {
      barWidth: 10,
      barMargin: 5,
      barFont: 10,
    };
  },

  watch: {
    immediate: true,
    deep: true,
    newArray(newArray) {
      // watch it if array change
      // console.log(newArray);
      this.barWidth = 1000 / newArray.length;
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
  /* width: 10px; */
  background: #6299f1;
  position: relative;
  left: 5%;
  /* margin: 5px; */
  float: left;
}
.active {
  background-color: red;
}
</style>
