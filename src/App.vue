<template>
  <div>
    <h2>To do List</h2>
    <add-task @inputValue="addTask"></add-task>
    <list-task v-for="task in taskList" :key="task.id" :name="task.name" @removeTask="removeTask(task.id)"></list-task>
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
      taskList:[
        {id: 1,name: 'buy groceries'},
        {id:2,name:'wash the car'},
        {id:3,name:'play video games'}
      ]
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
    }
  },
  provide(){
    return{
      removeTask: this.taskList.id
    };
  },
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
