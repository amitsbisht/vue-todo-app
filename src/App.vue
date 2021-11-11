<template>
  <main>
    <todo-header/>
		<todo-form @addTodo="addTodo" />
		<todo-list :todos="todos" @toggleTodo="toggleTodo" @removeTodo="removeTodo" />
    <todo-footer/>
  </main>
</template>

<script>
import TodoHeader from '@/components/TodoHeader.vue';
import TodoForm from '@/components/TodoForm.vue';
import TodoList from '@/components/TodoList.vue';
import TodoFooter from '@/components/TodoFooter.vue';

export default {
  name: 'App',
  components: {
    TodoHeader,
    TodoForm,
    TodoList,
    TodoFooter,
  },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    addTodo(todo) {
      if (!todo.trim()) return;
      const newTodo = {
        value: todo,
        isCompleted: false,
      };
      this.todos.push(newTodo);
    },
    toggleTodo(index) {
      this.todos[index].isCompleted = !this.todos[index].isCompleted;
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
  },
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Rubik:wght@300;400;600;800&display=swap');

*,
*::before,
*::after {
	box-sizing: border-box;
}

body {
	margin: 0;
	font-family: 'Rubik', sans-serif;
}

#app {
  max-width: 500px;
	margin: 0 auto;
	display: flex;
	justify-content: center;
	flex-direction: column;

	main {
		background-color: #4caf50;
    padding: 15px;
	}
}
</style>
