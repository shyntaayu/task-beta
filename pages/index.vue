<template>
  <div class="py-4">
    <div class="container">
      <div
        class="title border-bottom d-flex align-items-center justify-content-between py-2"
      >
        <h5>Task</h5>
        <div class="d-flex align-items-center ms-auto">
          <div>
            <b-dropdown id="dropdown-1" text="Category" class="m-md-2">
              <b-dropdown-item
                v-for="(item, i) in resultCategory"
                :key="i"
                @click="cat = item"
                >{{ item }}</b-dropdown-item
              >
            </b-dropdown>
          </div>
          <!-- /* Form input pencarian */ -->
          <input
            type="text"
            class="form-control"
            placeholder="Search"
            v-model="searchQuery"
          />
          <div class="d-flex align-items-center justify-content-end w-100">
            <span class="me-2">View As</span>
            <button
              class="btn btn-outline-secondary py-1 px-3"
              @click="isGrid = !isGrid"
            >
              {{ isGrid ? "Grid" : "List" }}
            </button>
          </div>
        </div>
      </div>

      <div class="list-task row">
        <CardItem
          v-for="(item, i) in resultQuery"
          :key="i"
          :task="item"
          :isGrid="isGrid"
        />
      </div>

      <div class="action py-2">
        <!-- /* Jika isCreating == false maka tombol Add Task tidak akan tampil */
	/* isCreating = !isCreating berfungsi sebagai switcher toggle */ -->
        <a
          href="#"
          class="add-button"
          v-if="!isCreating"
          @click="isCreating = !isCreating"
          >Add Task</a
        >
        <div class="add-card" v-else>
          <div class="card mb-2">
            <div class="card-body d-flex flex-column p-0">
              <input
                class="form-control border-0 mb-2"
                placeholder="Title"
                type="text"
              />
              <textarea
                class="form-control border-0 small"
                placeholder="Description"
                rows="3"
              ></textarea>
            </div>
          </div>
          <div class="button-wrapper d-flex">
            <button class="btn btn-primary me-2">Save</button>
            <button
              class="btn btn-outline-secondary"
              @click="isCreating = !isCreating"
            >
              Cancel
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import CardItem from "@/components/Card/CardItem.vue";
export default {
  components: {
    CardItem,
  },
  data() {
    return {
      //var penampung teks pencarian
      searchQuery: "",
      tasks: [
        {
          title: "Task 1",
          description: "ini deskripsi task 1",
          isDone: false,
          category: "Daily",
        },
        {
          title: "Task 2",
          description: "ini deskripsi 2",
          isDone: false,
          category: "BiWeekly",
        },
        {
          title: "Task 3",
          description: " ini deskripsi 3",
          isDone: false,
          category: "Daily",
        },
        {
          title: "Task 4",
          description: "ini deskripsi task 4",
          isDone: false,
          category: "BiWeekly",
        },
        {
          title: "Task 5",
          description: "ini deskripsi 5",
          isDone: false,
          category: "Weekly",
        },
        {
          title: "Task 6",
          description: " ini deskripsi 6",
          isDone: false,
          category: "Daily",
        },
      ],
      //status saat menambah task
      isCreating: false,
      // Tipe layout daftar task
      isGrid: false,
      cat: "",
    };
  },
  computed: {
    resultQuery() {
      if (this.cat != "")
        return this.tasks.filter((i) => i.category == this.cat);
      if (this.searchQuery) {
        return this.tasks.filter((i) => {
          return this.searchQuery
            .toLowerCase()
            .split(" ")
            .every((v) => i.title.toLowerCase().includes(v));
        });
      } else {
        console.log(this.tasks);
        return this.tasks;
      }
    },

    resultCategory() {
      let a = this.tasks
        .map((item) => item.category)
        .filter((value, index, self) => self.indexOf(value) === index);
      console.log(a);
      return a;
    },
  },
  methods: {},
};
</script>

<style>
.red {
  color: blue;
}
</style>
