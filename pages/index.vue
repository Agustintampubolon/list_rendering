<template>
  <div class="py-4">
    <div class="container">
      <div
        class="title border-bottom d-flex align-items-center justify-content-between py-2"
      >
        <h5>Task</h5>

        <div class="d-flex align-items-center ms-auto">
          <button
            class="btn btn-outline-primary py-1 px-3 me-4"
            @click="shuffle"
          >
            Shuffle!
          </button>
          <input
            type="text"
            class="form-control py-1 px-3 me-2"
            placeholder="Search Title"
            v-model="searchQuery"
          />

          <div class="d-flex align-items-center">
            <button
              class="btn btn-outline-secondary py-1 px-3 me-3"
              @click="isGrid = !isGrid"
            >
              {{ isGrid ? "Grid" : "List" }}
            </button>
          </div>
        </div>
        <div class="select">
          <select
            name="sortBy"
            class="form-control py-1 px-7 me-4"
            id="select"
            v-model="sortBy"
          >
            <option value="" disabled>Sort Tasks By</option>
            <option value="ascending">Title (A-Z)</option>
            <option value="descending">Title (Z-A)</option>
          </select>
        </div>
      </div>

      <transition-group name="tasks" tag="div" class="list-task row">
        <CardItem
          v-for="task in filteredTasks"
          :key="task.id"
          :task="task"
          :isGrid="isGrid"
        />
      </transition-group>
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
      sortBy: "",

      searchQuery: "",

      isGrid: false,

      arrayOfObjects: [],

      tasks: [
        {
          id: 1,
          title: "Lemper",
          description: "Lemper Enak",
          isDone: false,
          category: "Makanan",
          selected: "",
        },
        {
          id: 2,
          title: "Teh Bohai",
          description: "Teh Bohai Seger",
          isDone: false,
          category: "Minuman",
          selected: "",
        },
        {
          id: 3,
          title: "Mintz",
          description: "Mintz Seger",
          isDone: false,
          category: "Permen",
          selected: "",
        },
        {
          id: 4,
          title: "Jagung",
          description: "Jagung Di Bakar",
          isDone: false,
          category: "Makanan",
        },
        {
          id: 5,
          title: "Cincau",
          description: "Cincau Bikin Lengket",
          isDone: false,
          category: "Minuman",
        },
        {
          id: 6,
          title: "Kopiko",
          description: "Kopiko Adem",
          isDone: false,
          category: "Permen",
        },
      ],
    };
  },

  methods: {
    shuffle() {
      this.tasks = _.shuffle(this.tasks);
    },
  },
  computed: {
    resultQuery() {
      if (this.selected) {
        return this.tasks.filter((item) => {
          return this.selected
            .toLowerCase()
            .split(" ")
            .every((v) => item.category.toLowerCase().includes(v));
        });
      } else {
        console.log(this.tasks);
        return this.tasks;
      }
    },

    filteredTasks() {
      if (this.searchQuery != "" && this.searchQuery) {
        return this.tasks.filter((tasks) => {
          return tasks.title
            .toUpperCase()
            .includes(this.searchQuery.toUpperCase());
        });
      }

      return this.tasks.sort((a, b) => {
        if (this.sortBy == "ascending") {
          if (a.title.toLowerCase() < b.title.toLowerCase()) {
            return -1;
          }
          if (a.title.toLowerCase() > b.title.toLowerCase()) {
            return 1;
          }
          return 0;
        } else if (this.sortBy == "descending") {
          if (a.title.toLowerCase() > b.title.toLowerCase()) {
            return -1;
          }
          if (a.title.toLowerCase() < b.title.toLowerCase()) {
            return 1;
          }
          return 0;
        } else {
          return this.tasks;
        }
      });
    },
  },
};
</script>

<style>
.my-dropdown-toggle {
  border-radius: 5px;
}
.tasks-move {
  transition: 0.4s;
}
select {
  -webkit-appearance: none;
  -moz-appearance: none;
  background: transparent;
  background-image: url("data:image/svg+xml;utf8,<svg fill='black' height='24' viewBox='0 0 24 24' width='24' xmlns='http://www.w3.org/2000/svg'><path d='M7 10l5 5 5-5z'/><path d='M0 0h24v24H0z' fill='none'/></svg>");
  background-repeat: no-repeat;
  background-position-x: 100%;
  background-position-y: 5px;
  border: 1px solid #dfdfdf;
  border-radius: 2px;
  margin-right: 2rem;
  padding: 1rem;
  padding-right: 2rem;
}
</style>
