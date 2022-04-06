<template>
  <div class="hello">
    <h1>{{ count }}</h1>
    <h2>{{ totalMarks }}</h2>
    <h3 v-if="display">Display Conditionally</h3>
    <button @click="isDisplay = !isDisplay">Toggle</button>
  </div>
</template>
<script>
import Button from "~/components/Button.vue";
export default {
  components: { Button },
  data() {
    return {
      shopNumber: 2,
      number: 3,
      isDisplay: true,
    };
  },
  computed: {
    count: function () {
      return "The shop number is " + this.shopNumber;
    },
    totalMarks() {
      return this.number * 2;
    },
    display() {
      if (this.isDisplay) return true;
      else return false;
    },
  },
};
</script>
