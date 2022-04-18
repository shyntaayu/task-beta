<template>
  <div>
    <p id="life">{{ msg }}</p>
    <button class="btn btn-success" @click="msg = 'text berubah'">
      Update
    </button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      msg: "text awal",
    };
  },
  beforeCreate() {
    console.log("before create");
    // console.log(document.getElementById("life"));
  },
  created() {
    console.log("created");
    console.log(this.msg);
    console.log(document.getElementById("life"));
  },
  beforeMount() {
    console.log("before mount");
    console.log(document.getElementById("life"));
  },
  mounted() {
    console.log("mounted");
    console.log(document.getElementById("life"));
  },
  beforeUpdate() {
    console.log("before update");
    console.log(document.getElementById("life").textContent);
  },
  updated() {
    console.log("updated");
    console.log(document.getElementById("life").textContent);
  },
  beforeUnmount() {
    console.log("before unmount");
  },
  unMounted() {
    console.log("unmounted");
  },
};
</script>
