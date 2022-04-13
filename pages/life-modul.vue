<template>
  <div>
    <div ref="example-element">{{ counter }}</div>
    <h1>{{ num }}</h1>
    <button class="btn btn-success" @click="num += 1">Plus</button>
    <!-- <h2>{{ plus }}</h2> -->
    <!-- <div ref="example-element">{{ propertyComputed }}</div> -->
    <!-- <div ref="example-element">Example component.</div> -->
  </div>
</template>
<script>
export default {
  data() {
    return {
      num: 0,
      counter: 0,
      property: "Example property.",
      exampleLeakyProperty:
        "This represents a property that will leak memory if not cleaned up.",
    };
  },

  computed: {
    propertyComputed() {
      return this.property;
    },
  },

  methods: {
    plus() {
      console.log("jalankan plus()");
      this.num++;
    },
  },

  beforeCreate() {
    //sebeum dirender
    console.log(
      "beforecreated-At this point, events and lifecycle have been initialized."
    );
    console.log("this.num", this.num);
  },

  created() {
    //sebeum dirender
    // this.plus();
    console.log(
      "created-At this point, this.property is now reactive and propertyComputed will update."
    );
    this.property = "Example property updated.";
    console.log("this.num", this.num);
  },

  beforeMount() {
    //berhasil dirender
    console.log(`beforemount-At this point, vm.$el has not been created yet.`);
    console.log("this.num", this.num);
  },

  mounted() {
    //berhasil dirender
    // setInterval(() => {
    //   this.counter++;
    // }, 1000);
    console.log(
      `mounted-At this point, vm.$el has been created and el has been replaced.`
    );
    console.log(this.$el.textContent); // Example component.
    console.log("this.num", this.num);
  },

  beforeUpdate() {
    //render ulang, ketika ada perubahan data
    console.log(
      `beforeupdate-At this point, Virtual DOM has not re-rendered or patched yet.`
    );
    // Logs the counter value every second, before the DOM updates.
    console.log(this.counter);
    console.log(
      "beforeupdate",
      +this.$refs["example-element"].textContent === this.counter
    );
    console.log("this.num", this.num);
  },

  updated() {
    //render ulang, ketika ada perubahan data
    console.log(
      `updated-At this point, Virtual DOM has re-rendered and patched.`
    );
    // Fired every second, should always be true
    console.log(
      "updated",
      +this.$refs["example-element"].textContent === this.counter
    );
    console.log("this.num", this.num);
  },

  beforeDestroy() {
    // dibuang/dihancurkan
    console.log(
      `At this point, watchers, child components, and event listeners have not been teared down yet.`
    );
    // Perform the teardown procedure for exampleLeakyProperty.
    // (In this case, effectively nothing)
    this.exampleLeakyProperty = null;
    delete this.exampleLeakyProperty;
  },
};
</script>
