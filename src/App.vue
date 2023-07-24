<template>
  <div>
    <h2>To do List</h2>
    <add-task @inputValue="addTask"></add-task>
    <list-task v-for="task in taskList" :key="task.id" :name="task.name" @removeTask="removeTask(task.id)" :taskId="task.id" @newId="setTaskId(task.id)" @newInput="setNewInput"></list-task>
  </div>
</template>

<script>
import ListTask from './components/ListTask.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    ListTask,
    AddTask
  }, 
  data(){
    return{
      inputValue:'',
      updatedInput:'buy groceries and fill up',
      taskList:[
        {id: 1,name: 'buy groceries'},
        {id:2,name:'wash the car'},
        {id:3,name:'play video games'}
      ]
    }
  },
  watch: {
    updatedTask(newTask) { // Modify the watch to receive the updated task object
      if (this.selectedTaskId !== null && newTask !== null && newTask.name !== '') {
        const taskToUpdate = this.taskList.find((task) => task.id === this.selectedTaskId);
        if (taskToUpdate) {
          taskToUpdate.name = newTask.name; // Use the new task name to update the task's name.
          this.updatedTask = null; // Reset the updated task object once it's been applied
        }
      }
    }
  },
  methods:{
    addTask(input){
      const newTask = {
        id : new Date().toString(),
        name: input
      };
      this.taskList.push(newTask)
    },
    removeTask(taskId){
      this.taskList = this.taskList.filter((task)=> task.id !== taskId)
    },
    setNewInput(newName){
      this.updatedInput = newName;
    },
    setTaskId(newId){
      const taskToUpdate = this.taskList.find((task) => task.id === newId);
      if (taskToUpdate) {
        taskToUpdate.name = this.updatedInput;
      }
    },
    editTask(taskId, newName){
      //this.taskList = this.taskList.filter((task)=> task.id !== taskId)
      //this.taskList.push({id:taskId,name:newName})
      const taskToUpdate = this.taskList.find((task) => task.id === taskId);
      if (taskToUpdate) {
        taskToUpdate.name = newName;
      }
      //const updateTask = this.taskList.find((task)=> task.id === taskId)
      //updateTask.name = newName;
    }
  }
}
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
