<template>
  <div class="py-4">
    <div v-if="isLoading" class="container text-center">
      <img src="/loading.gif" />
    </div>
    <div class="container" v-else>
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
                >{{ item == "" ? "Nothing selected" : item }}</b-dropdown-item
              >
            </b-dropdown>
          </div>
          <button class="btn btn-danger me-2" @click="isShow = !isShow">
            {{ !isShow ? "Show" : "Hide" }}
          </button>

          <button
            class="btn btn-outline-primary py-1 px-3 me-4"
            @click="shuffle"
          >
            Shuffle!
          </button>

          <button class="btn btn-success me-4" @click="sortMe">
            Sort {{ isAsc ? "Asc" : "Desc" }}
          </button>

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

      <transition-group name="tasks" tag="div" class="list-task row">
        <CardItem
          v-for="(item, i) in resultQuery"
          :key="item.id"
          :task="item"
          :isGrid="isGrid"
          :isShow="isShow"
        />
      </transition-group>

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
          <form v-on:submit.prevent="handleSubmit">
            <div class="card mb-2">
              <div class="card-body d-flex flex-column p-0">
                <input
                  class="form-control border-0 mb-2"
                  placeholder="Title"
                  type="text"
                  v-model="form.title"
                  autofocus
                />
                <textarea
                  class="form-control border-0 small"
                  placeholder="Description"
                  v-model="form.description"
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
          </form>
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
          id: 1,
          title: "Task 1",
          description: "ini deskripsi task 1",
          isDone: false,
          category: "Daily",
        },
        {
          id: 2,
          title: "Task 2",
          description: "ini deskripsi 2",
          isDone: false,
          category: "BiWeekly",
        },
        {
          id: 3,
          title: "Task 3",
          description: " ini deskripsi 3",
          isDone: false,
          category: "Daily",
        },
        {
          id: 4,
          title: "Task 4",
          description: "ini deskripsi task 4",
          isDone: false,
          category: "BiWeekly",
        },
        {
          id: 5,
          title: "Task 5",
          description: "ini deskripsi 5",
          isDone: false,
          category: "Weekly",
        },
        {
          id: 6,
          title: "Task 6",
          description: " ini deskripsi 6",
          isDone: false,
          category: "Daily",
        },
        {
          id: 7,
          title: "ada",
          description: " ini deskripsi 6",
          isDone: false,
          category: "Daily",
          image: "/assets/emas.png",
        },
        {
          id: 8,
          title: "xyz",
          description: " ini deskripsi 6",
          isDone: false,
          category: "Daily",
        },
      ],
      //status saat menambah task
      isCreating: false,
      // Tipe layout daftar task
      isGrid: false,
      cat: "Nothing selected",
      isShow: false,
      isLoading: true,
      form: {
        title: "",
        description: "",
        isDone: false,
        category: "New",
      },
      isAsc: true,
    };
  },
  computed: {
    resultQuery() {
      if (this.cat != "Nothing selected")
        return this.tasks.filter((i) => i.category == this.cat);
      else if (this.cat == "Nothing selected") return this.tasks;
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
      a.push("Nothing selected");
      console.log(a);
      return a;
    },
  },
  methods: {
    handleSubmit() {
      console.log(this.form);
      this.tasks.push(this.form);
      this.isCreating = false;
    },
    shuffle() {
      this.tasks = _.shuffle(this.tasks);
    },
    sortMe() {
      if (this.isAsc) {
        this.tasks = this.tasks.sort((a, b) => (a.title > b.title ? 1 : -1));
      } else {
        this.tasks = this.tasks.sort((a, b) => (a.title > b.title ? -1 : 1));
      }
      this.isAsc = !this.isAsc;
    },
  },
  mounted() {
    setTimeout(() => {
      this.isLoading = false;
    }, 1000);
  },
  created() {
    // if (localStorage.getItem("task-me") != undefined)
    //   this.tasks = localStorage.getItem("task-me");
  },
  updated() {
    // localStorage.setItem("task-me", this.tasks);
  },
};
</script>

<style>
.red {
  color: blue;
}
.tasks-move {
  transition: 0.4s;
}
</style>
