<template>
  <div id="app">
    <h4 class="bg-primary text-white text-center p-3">
      {{name}}`s TodoApplication
    </h4>
      <div class="container-fluid p-4">
        <div class="row" v-if="filteredTasks.length == 0">
          <div class="col text-center">
            <b>Nothing to do. Hurrah!</b>
          </div>
        </div>
        <template v-else>
        <div class="row">
          <div class="col font-weight-bold">
            Task
          </div>
          <div class="col-2 font-weihgt-bold">
            Done
          </div>
        </div>
        <div class="row" v-for="task in filteredTasks" :key="task.action">
          <div class="col">{{task.action}}</div>
          <div class="col-2 text-center">
            <input type="checkbox" v-model="task.done" 
            class="form-check-input">
            </div>
        </div>
        </template>

        <div class="row py-2">
          <div class="col">
            <input v-model="newItemText" class="form-control">
          </div>
          <div class="col-2">
            <button class="btn btn-primary" @click="addNewTodo">Add</button>
          </div>
        </div>
         <div class="row bg-primary py-2 mt-2 text-white">
          <div class="col text-center">
            <input type="checkbox" name="" id="" v-model="hideCompleted" class="form-check-input">
            <label for="" class="form-check-label font-weight-bold">
              Hide completed tasks 
            </label>
          </div>
          <div class="col text-center">
            <button class="btn btn-sm btn-warning"
              @click="deleteCompleted">
              Delete Completed
            </button>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      name: 'Tshatmanaliev',
      tasks: [],
      hideCompleted: true,
      newItemText: ""
    }
  },
  computed: {
    filteredTasks() {
      return this.hideCompleted ?
       this.tasks.filter(task => !task.done) : this.tasks
    }
  },
  methods: {
    addNewTodo() {
      this.tasks.push({
        action: this.newItemText,
        done: false
      });
      this.storeData();
      this.newItemText = "";

    },
    storeData() {
      localStorage.setItem("todos", JSON.stringify(this.tasks));
    },
    deleteCompleted() {
      this.tasks = this.tasks.filter(task => ! task.done);
      this.storeData();
    }
  },
  created() {
    let data = localStorage.getItem("todos");
    if(data != null) {
      this.tasks = JSON.parse(data);
    }
  }
}
</script>

<style scoped>

</style>
