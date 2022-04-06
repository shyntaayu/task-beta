<template>
  <div>
    <h1 v-if="num == 0">Angkanya 0</h1>
    <h1 v-else-if="num > 0">Angkanya positif</h1>
    <h1 v-else-if="num < 0">Angkanya negatif</h1>
    <h1 v-else>Bukan angka 0</h1>

    <h1>Title</h1>
    <p>Paragraph 1</p>
    <p>Paragraph 2</p>
    <div v-if="ok">
      <label>Username</label>
      <input placeholder="Enter your username" key="username-input" />
    </div>
    <div v-else>
      <label>Email</label>
      <input placeholder="Enter your email address" key="username-input" />
    </div>
    <button @click="ok = !ok">Toggle OK</button>
    <h1 v-show="ok">Ini Pake V-SHow</h1>
  </div>
</template>

<script>
export default {
  data() {
    return {
      num: "-4 aa",
      ok: false,
    };
  },
};
</script>
