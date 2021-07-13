<template>
  <div class="container mt-5">
    <div class="row justify-content-center">
      <div class="col-12 col-md-6">
        <img alt="Vue logo" src="./assets/logo.png">
        <h1>What ya gonna do today mate?¿</h1>
        <h5 class="m-5">Write down your list for today</h5>
      </div>
    </div>
  </div>

  <div class="container mt-5">
    <div class="row justify-content-center">
      <div class="ccol-12 col-md-6">
        <form @submit.prevent="addNewTodo">
          <div class="input-group">
            <input v-model="newTodo" type="text" name="newTodo" class="form-control text-center mb-5 "
              placeholder="Write here">
            <div class="input-group-append" id="button-addon4">
              <button class="btn btn-primary" type="submit">Send</button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>

  <div class="container">
    <div class="row justify-content-center">
      <div class="col-12 col-md-6">
        <div class="card border-0" v-for="(todo,index) in todos" v-bind:key="todo.id">
          <div class="card-body shadow">
            <div class=" card-title" :class="{ 'done' : todo.done}">
              {{  todo.content }}
            </div>
          </div>

          <div class="d-flex justify-content-center m-5">
            <button @click="toggleDown(todo)" class="btn btn-success m-3">Done</button>
            <button @click="removeTodo(index)" class="btn btn-danger m-3">Delete</button>
          </div>

        </div>
      </div>
    </div>
  </div>

<div style="margin-top: 1000px"></div>
</template>

<script>
  import {
    ref
  } from 'vue';

  export default {
    setup() {
      const newTodo = ref('');
      const todos = ref([]);

      function addNewTodo() {
        todos.value.push({
          id: Date.now(),
          done: false,
          content: newTodo.value,
        });
        newTodo.value = '';
      }

      function toggleDown(todo) {
        todo.done = !todo.done;
      }

      function removeTodo(index) {
        todos.value.splice(index, 1);
      }

      return {
        newTodo,
        todos,
        addNewTodo,
        toggleDown,
        removeTodo,
      }
    },
  }
</script>

<style>

  #app {
    font-family: Avenir, 'Jura', sans-serif;
    
    text-align: center;
    
  }


  .done {
    text-decoration: line-through;
  }

</style>