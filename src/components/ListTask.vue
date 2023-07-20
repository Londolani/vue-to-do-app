<template>
    <div class="card">
      <div class="card-header">
        <strike v-if="strike"><p>{{ name }}</p></strike>
        <p v-if="!strike">{{ name }}</p>
        <div class="buttons">
            <button class="done-button" @click="done"> {{ strike ? 'undo':'done'}}</button>
            <button class="edit-button" @click="editTask(id)">Edit</button>
            <button class="remove-button" @click="removeTask(id)">Remove</button>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: ['name', 'id'],
    data(){
        return{
            strike:false,
            doneButton: 'Done'
        }
    },
    methods: {
      editTask(id) {
        this.$emit('editTask', id);
      },
      removeTask(id) {
        this.$emit('removeTask', id);
      },
      done(){
        this.strike = !this.strike;
        this.button = 'undo'
      }
    },
  };
  </script>
  
  <style scoped>
  .card {
    border: 1px solid #ccc;
    border-radius: 10px;
    padding: 10px;
    margin-bottom: 10px;
    border-color: #4CAF50;
  }

  .card-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
    }
  
  p {
    font-size: 18px;
    margin: 0;
    padding: 10px;
  }
  
  .buttons {
    display: flex;
    align-items: center;
  }
  
  button {
    padding: 8px 16px;
    margin-left: 8px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .edit-button {
    background-color: green;
    color: #fff;
  }
  
  .remove-button {
    background-color: red;
    color: #fff;
  }
  
  .done-button {
    background-color: black;
    color: #fff;
  }
  </style>
  