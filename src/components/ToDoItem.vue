<template>
    <div class="todoParent">
        <div class="boutonDone" @click="statutTodo(todo)">Done</div>
        <p class="ToDoItem-Text" v-bind:class="{ success: isActive}">{{todo.text}}</p>
        <div class="boutonDelete"
             @click="deleteItem(todo)">-
        </div>
    </div>
</template>

<script>
    export default {
        name: "to-do-item",
        props: ['todo'],
        data(){
          return {
            isActive:false
          }
        },
        methods: {
            deleteItem(todo) {
                this.$emit('delete', todo)
            },
            statutTodo(todo) {
              // Quand je clique sur le bouton ca change le texte en vert
              this.isActive = true,
              console.log(todo.text)
              // this.$emit('done', todo)
            }
        }
    }
</script>

<style>
.success {
  color:green;
}
    .todoParent {
        display: flex;
        justify-content: space-between;
        align-items: center;
        border-bottom: 1px solid #DDD;
    }
    .ToDoItem-Text {
        padding: 12px;
        margin-right: 10px;
    }
    .boutonDone {
      padding: 5px;
      height: 20px;
      cursor: pointer;
      background: #ff6d05;
      border-radius: 10px;
      box-shadow: 1px 1px 1px #c70202;
      color: white;
      font-size: 18px;
      margin-right: 5px;
    }
    .boutonDone:hover {
        box-shadow: none;
        margin-top: 1px;
        margin-left: 1px;
    }
    .boutonDelete {
        width: 20px;
        padding: 5px;
        height: 20px;
        cursor: pointer;
        background: #ff7373;
        border-radius: 10px;
        box-shadow: 1px 1px 1px #c70202;
        color: white;
        font-size: 18px;
        margin-right: 5px;
    }
    .boutonDelete:hover {
        box-shadow: none;
        margin-top: 1px;
        margin-left: 1px;
    }
</style>