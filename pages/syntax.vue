<template>
  <div class="py-4">
    <div class="container">
      <div class="title border-bottom">
        <h5 class="red">Task</h5>
        <p class="blue">item-task d-flex align-items-center border-bo</p>
      </div>

      <div class="list-task">
        <div
          class="item-task d-flex align-items-center border-bottom pt-3 pb-4"
        >
          <input type="checkbox" name="status" id="task" class="me-2" />
          <div class="title-task">Tugas 1</div>
        </div>
      </div>

      <div class="action py-2">
        <a href="#" class="add-button">Add Task</a>
      </div>
      <br />
      <h5>Pembelajaran {{ msg }}</h5>
      {{ msg }}
      <div>{{ topic }}</div>
      <span v-once>{{ msg }}</span>

      <p>Menggunakan kurung kurawal: {{ rawHtml }}</p>
      <p>Menggunakan v-html directive: <span v-html="rawHtml"></span></p>
      <div>
        <button v-bind:disabled="isButtonDisabled">Button</button>

        {{ number + 1 }}

        {{ ok ? "YES" : "NO" }}

        {{ msg.split("").reverse().join("") }}

        <div v-bind:id="'list-' + id">lalala</div>

        <p v-if="seen">Now you see me</p>
        <p v-if="!seen">seen is {{ seen }}</p>

        <a v-bind:href="url"> argumen </a>

        <a v-on:click="doSomething"> onclick </a>

        <a v-bind:[attributeName]="url"> attributeName </a>

        <a v-on:[eventName]="doSomething"> ... </a>

        <hr />
        <!-- full syntax -->
        <a v-bind:href="url"> ... </a> <br />
        <!-- shorthand -->
        <a :href="url" target="_blank"> ... new tab </a> <br />
        <!-- shorthand dengan argumen dinamis (2.6.0+) → -->
        <a :[attributeName]="url"> ... </a>

        <hr />
        <!-- full syntax -->
        <a v-on:click="doSomething"> ... </a>
        <!-- shorthand -->
        <a @click="doSomething"> ... </a>
        <!-- shorthand dengan argumen dinamis (2.6.0+) -->
        <a @[eventName]="doSomething"> ... </a>

        <hr />
        <h1>Styling</h1>
        <div v-bind:class="{ active: isActive }">style</div>
        <div
          class="static"
          :class="{ active: data.isActive, 'text-danger': data.hasError }"
        >
          style
        </div>

        <div :class="classObject">style classObject</div>
        <hr />
        <div v-bind:class="[activeClass, errorClass]">array syntax</div>
        <div v-bind:class="[multiClass]">array syntax</div>
        <div v-bind:class="[isActive ? activeClass : '', errorClass]">
          ternary
        </div>

        <div
          v-bind:class="[
            { active: isActive, lead: isButtonDisabled },
            errorClass,
          ]"
        >
          array object
        </div>
        <br />
        <hr />
        <div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }">
          binding style
        </div>
        <div v-bind:style="styleObject">styleObject</div>
        <div v-bind:style="{ color: ['black', 'red', 'green'] }">
          Color Text
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      activeColor: "red",
      fontSize: 30,

      styleObject: {
        color: "red",
        fontSize: "13px",
      },

      msg: "rabu sore, habis hujan, eeee",
      topic: "pertamax naik 16000",
      rawHtml:
        '<div class="action py-2"><a href="#" class="add-button">Add Task untuk rawa</a></div>',
      isButtonDisabled: true,
      number: 100,
      ok: false,
      id: 13,
      seen: false,
      url: "https://content.nuxtjs.org/writing/",
      attributeName: "href",
      eventName: "click",
      isActive: true,
      hasError: true,
      data: {
        //variabel aja
        isActive: true,
        hasError: true,
      },
      classObject: {
        //nama class
        active: true,
        "text-success": true,
      },
      activeClass: "active",
      errorClass: "text-danger",
      multiClass: "bg-light text-warning",
    };
  },

  methods: {
    doSomething() {
      alert("hai rabu");
    },
  },
};
</script>

<style>
.red {
  color: blue;
}
.active {
  background: yellow;
}
</style>
