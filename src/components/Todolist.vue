<template>
    <div>
        todo list
        <input 
            type="text" 
            class="todo-input" 
            placeholder="type a task"
            v-model="newTask"
            @keyup.enter="addTask">
        <div v-for="(todo, index) in todos" :key="todo.id" class="todo-item"> 
            <div> {{ todo.text }} </div> 
            <div 
                class="remove-item"
                @click="removeTask(index)">
                &times;
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'TodoList',
  data: function () {
      return {newTask: '',
      todos: [
          {
              'id': 1,
              'text': 'finish this app!',
              'completed': false
          },
          {
              'id': 2,
              'text': 'GO HOME',
              'completed': false
          }
      ],
      taskID: 3,
    }
  },
  methods: {
      addTask () {
          if(this.newTask.trim().length === 0) {
              return;
          }

          this.todos.push({
              id: this.taskID,
              text: this.newTask,
              completed: false
          })

          this.newTask = '';
          this.taskID++;

          console.log("updated todos ", this.todos);
      },
      removeTask (index) {
          this.todos.splice(index, 1);
          console.log("updated todos ", this.todos);
      }
  },
  props: {
  }
}
</script>

<style lang="scss">
.todo-input {
    width: 100%;
    padding: 10px 18px;
    font-size: 18px;
    margin-bottom: 16px;

    &:focus {
        outline: 0;
    }
}

.todo-item {
    margin-bottom: 12px;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.remove-item {
    cursor: pointer;
    margin-left: 14px;
    &:hover {
        color: red;
    }
}
</style>
