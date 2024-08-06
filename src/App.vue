<script setup>
  import { ref } from 'vue';
  const newTodo = ref('');
  const todos = ref([])
// export default {
  // setup() {
      function addNewTodo() {
        if (newTodo.value=='') {
          alert("You can't add an empty task")
        } else {
          todos.value.push({
            id: Date.now(),
            done : false,
            content : newTodo.value
          });
        }
        newTodo.value='';
      }
      function toggleDone(todo) {
        // document.getElementById('hy').style.textDecoration="dashed"
        todo.done = !todo.done
      }
      function deleteTache(index) {
        todos.value.splice(index, 1)
      }
      function markAllDone() {
        todos.value.forEach((todo) => todo.done = true);
      }
      function removeAll() {
        todos.value=[]
      }
    // return {
    //   addNewTodo,
    // };
  // }  

// }
</script>

<template>
  <section>
    <h1>Vue 3 Todo App</h1>
    <form @submit.prevent="addNewTodo">
      <label>New Todo</label>
      <input v-model="newTodo" name="newTodo">
      <button class="add">Add New Todo</button>
    </form>
    <button class="mark" @click="markAllDone">Mark all done</button>
    <button class="remove" @click="removeAll">Remove all</button>
    <ul>
      <li class="todo" v-for="(todo, index) in todos" :key="todo.id">
        <h3 :class="{done : todo.done}" @click="toggleDone(todo)">{{ todo.content  }}</h3>
        <button class="delete" @click="deleteTache(index)">Delete</button>
      </li>
    </ul>
  </section>
  <!-- <h2>{{ newTodo }}</h2> -->
</template>

<style scoped>
  body {
    font-family: sans-serif;
    padding-top: 1em;
    padding-bottom: 1em;
    font-size: 2em;
    width: 80%;
    margin: 0 auto; 
    /* text-decoration: dashed; */
  }
  section{
    margin: 0 auto; 
    padding-top: 20px;
    /* border: 2px solid blue; */
    background-color: beige;
    border-radius: 10px;
    width: 600px;
    text-align: center;
  }
  h1{
    font-size: 35px;
  }
 form{
    display: flex;
    flex-direction: column;
    justify-content: center;
  }
  input, textarea, button{
    display: 'block';
    width: 70%;
    height: 30px;
    border-radius: 10px;
    font-family: sans-serif;
    font-size: 1em;
    margin: 10px auto;
  }
  ul{
    text-align: left;
    margin-left: 55px;
  }
  .todo {
    cursor: pointer;
  }

  .done {
    text-decoration: line-through;
  }
  .mark, .remove{
    width: 185px;
  }
  .remove{
    background-color: red;
    margin-left: 30px
  }
  .add{
    background-color: blue;
  }
  button{
    background-color: green;
    color: white;
    height: 35px;
    color: white;
    font-weight: bold;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  button:active{
    transform: scale(1.1);
  }
  .delete{
    width: 100px;
    height: 35px;
    background-color: red;
  }
</style>
