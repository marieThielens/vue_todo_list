<template>
  <div id="app">
    <div class="ToDo">
      <img class="Logo" :src="logo" alt="Vue logo"/>
      <h1 class="todoTitre">Todo List avec Vue.js</h1>
      <div class="papaInput">
        <!-- Input appyer sur enter ou cliquer sur le bouton pour créer un élement, une tâche à faire -->
        <input type="text" placeholder="Tâche à rajouter" v-model="todo" v-on:keyup.enter="creerElement"/>
        <div class="boutonRajouter" @click="creerElement()">+</div>
      </div>

      <div class="todoPapa">
        <div class="ToDo-Content">
          <ToDoItem v-for="todo in tableauTodo" 
                    :todo="todo" 
                    @delete="onDeleteItem"
                    :key="todo.id" />
        </div>

      </div>
    </div>
  </div>
</template>

<script>
import ToDoItem from './components/ToDoItem.vue'
import Logo from './assets/logo.png';
export default {
  name: 'to-do',
  components: {
    ToDoItem
  },
  data() {
      return {
          tableauTodo: [
              {
                id: 1,
                text: 'Apprendre React'
              },
              {
                id: 2,
                text: 'buy milk'
              }
          ],
          // tableauDone: [{}],
          todo: '',
          logo: Logo
      }
  },
  methods: {
      creerElement() {
        // Si todo n'est pas différent de sa position initiale (vide)
        if (!this.todo){
          alert("Vous n'avez rien écrit...");
          return
        }
        // ajouter l'element dans le tableau. id : la date (unique), text : 
        this.tableauTodo.push({ id: Date.now(), text: this.todo});
        this.todo = '';
      },
      onDeleteItem(todo){
        this.tableauTodo = this.tableauTodo.filter(item => item !== todo);
      }
      // onDoneElement(todo) {
      //   this.tableauDone.push({ id:this.todo.id, text: this.todo})
      //   console.log(tableauDone)
      // }
  },
}
</script>

<style>
  body {
    margin: 0;
    padding: 0;
    height: auto;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .Logo {
    width: 50px;
    position: relative;
    top: 50px;
  }
  .ToDo {
    text-align: center;
    border: 1px solid white;
    width: 80vw;
    height: auto;
    box-shadow: 2px 3px 15px rgba(0, 0, 0, 0.5);
    background: #f6f6f6;
    padding-bottom: 60px;
    margin: 40px auto;
  }
  .todoTitre {
    color: black;
    font-weight: 400;
    margin: 70px auto 30px;
  }
  .papaInput {
    display:flex;
    justify-content: space-around;
    width: 74%;
    margin: 0 auto;
  }
  .todoPapa {
  width: 80%;
  margin: 0 auto;
  }
  input {
    width: 57%;
    font-size: 1em;
    padding-left: 10px;
    /* box-shadow: 1px 3px 20px 0px rgba(0, 0, 0, 0.3) */
  }
  .boutonRajouter {
    color: white;
    font-size: 2em;
    width: 0.5em;
    height: 0.5em;
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 15px;
    cursor: pointer;
    background: #73ff73;
    border-radius: 10px;
    box-shadow: 1px 1px 1px #47a947;
  }
  .boutonRajouter:hover {
    box-shadow: none;
  }

</style>