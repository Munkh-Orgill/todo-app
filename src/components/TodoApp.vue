<template>
  <div class="container">
      <h2 class  = "text-center" mt-5>Vue Todo App</h2>
      <div class = "d-flex">
        <input v-model = "task" type="text" placeholder="Enter task" class="form-control">
        <button @click="submitTask" class="btn btn-warning rounded-0">SUBMIT</button>
      </div>

      <table class="table table-bordered mt-5">
        <thead>
          <tr>
            <th scope="col"></th>
            <th scope="col">Task</th>
            <th scope="col" class = text-center>#</th>
            <th scope="col" class = text-center>#</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(task, index) in tasks" :key="index">
            <td><input type="checkbox" v-model="task.done"></td>
            <td>
              <span :class = "{done: task.done}">{{task.name}}</span>
            </td>
            <td>
              <div class="text-center" @click="editTask(index)">
                <span class="fa fa-pen"></span>
              </div>
            </td>
            <td>
              <div class = "text-center" @click="deleteTask(index)">
                <span class="fa fa-trash"></span>
              </div>
            </td>
        </tr>       
        </tbody>
      </table>
    </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data(){
    return{
      task: '',
      editedTask: null,
      done: false,
      tasks: [
        {
          name: 'Steal bananas from the store',
        },

        {
          name: 'Drink 1l airag in 1 hour. ',
        }
      ]
    }
  },
    methods: {
      submitTask(){
        if(this.task.length === 0) return;

        if(this.editedTask === null){
          this.tasks.push({
            name: this.task,
            status: 'to-do'
          });
        }else{
          this.tasks[this.editedTask].name = this.task;
          this.editedTask = null;
        }

        this.task = '';
  
    },

    deleteTask(index){
      this.tasks.splice(index, 1);
    },

    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
  
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.done{
  text-decoration: line-through;
}
</style>
