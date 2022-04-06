<template>
  <div id="app">
    <Button :name="signedUp ? 'Logout' : 'Login'" bgColor="red" />
    <Button :name="btnName" bgColor="red" />
    <Button :name="btnName" bgColor="green" />
    <Button :name="btnName" bgColor="blue" />
  </div>
</template>
<script>
import Button from "@/components/Button";

export default {
  name: "App",
  data() {
    return {
      signedUp: true,
      btnName: "Joeeeloa",
    };
  },
  components: {
    Button,
  },
};
</script>
