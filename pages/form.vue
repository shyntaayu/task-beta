<template>
  <div class="container">
    <form v-on:submit.prevent="handleSubmit">
      <section class="form">
        <div class="mb-3">
          <label class="form-label">Name</label>
          <input
            v-model="form.name"
            class="form-control"
            type="text"
            placeholder="Name"
          />
        </div>
        <div class="mb-3">
          <label class="form-label">Message</label>
          <textarea
            class="form-control"
            placeholder="Message"
            v-model="form.message"
          ></textarea>
        </div>
        <div class="mb-3">
          <label class="form-label">Inquiry</label>
          <select v-model="form.inquiry_type" class="form-control">
            <option disabled value="">Nothing selected</option>
            <option
              v-for="option in options.inquiry"
              v-bind:value="option.value"
            >
              {{ option.text }}
            </option>
          </select>
        </div>
        <div class="mb-3">
          <label class="form-label">UseCase</label>
          <select multiple v-model="form.usecases" class="form-control">
            <option>Debugging</option>
            <option>Fixing Errors</option>
            <option>User support</option>
          </select>
        </div>
        <div class="mb-3 form-check">
          <label class="checkbox form-check-label">
            <input
              type="checkbox"
              class="form-check-input"
              v-model="form.terms"
            />
            I agree to the <a href="#">terms and conditions</a>
          </label>
        </div>
        <div>
          <div class="control form-check">
            <label class="checkbox form-check-label">
              <input
                type="checkbox"
                class="form-check-input"
                v-model="form.concepts"
                value="promises"
              />
              Promises
            </label>
            <label class="checkbox form-check-label">
              <input
                type="checkbox"
                class="form-check-input"
                v-model="form.concepts"
                value="testing"
              />
              Testing
            </label>
          </div>
        </div>
        <div>
          <div class="control form-check">
            <label class="radio form-check-label">
              <input
                v-model="form.js_awesome"
                class="form-check-input"
                type="radio"
                value="Yes"
              />
              Yes
            </label>
            <label class="radio form-check-label">
              <input
                v-model="form.js_awesome"
                class="form-check-input"
                type="radio"
                value="Yeap!"
              />
              Yeap!
            </label>
          </div>
        </div>
        <div class="field is-grouped">
          <div class="control">
            <button class="btn btn-primary">Submit</button>
          </div>
        </div>
      </section>
    </form>
    <section class="content">
      <ul>
        <li v-for="(item, k) in form">
          <strong>{{ k }}:</strong> {{ item }}
        </li>
      </ul>
    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: "",
        message: "",
        inquiry_type: "",
        usecases: [],
        terms: false,
        concepts: [], // nilai multiple checkbox
        js_awesome: "",
      },
      options: {
        inquiry: [
          { value: "feature", text: "Feature Request" },
          { value: "bug", text: "Bug Report" },
          { value: "support", text: "Support" },
        ],
      },
    };
  },
  methods: {
    handleSubmit() {
      console.log(this.form);
    },
  },
};
</script>
