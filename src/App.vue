<template>
	<main>
		<h1>Todooo App</h1>
		<section>
			<the-form @add="addTodo"></the-form>
		</section>
		<section>
			<ul class="todo-list" :class="{ active: todos.length > 0 }">
				<transition-group>
					<todo-item
						v-for="(todo, index) in todos"
						:key="index"
						:todo="todo"
						@toggle="toggleTodo"
						@remove="removeTodo"
					></todo-item>
				</transition-group>
			</ul>
		</section>
	</main>
</template>

<script>
	import TheForm from "./components/TheForm.vue";
	import TodoItem from "./components/TodoItem.vue";

	export default {
		name: "App",
		components: {
			TheForm,
			TodoItem,
		},
		data() {
			return {
				todos: [],
			};
		},
		methods: {
			addTodo(todo) {
				const newTodo = {
					name: todo,
					isCompleted: false,
				};
				this.todos.push(newTodo);
			},
			toggleTodo(todo) {
				todo.isCompleted = !todo.isCompleted;
			},
			removeTodo(todoToRemove) {
				const removeTodoIndex = this.todos.findIndex(
					(todo) => todo == todoToRemove
				);
				this.todos.splice(removeTodoIndex, 1);
			},
		},
	};
</script>

<style>
	@import url("https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,400;0,700;1,400&display=swap");
	*,
	*::before,
	*::after {
		box-sizing: border-box;
		margin: 0;
		padding: 0;
	}
	body,
	input,
	button {
		font-family: "Montserrat", sans-serif;
	}
	#app {
		max-width: 450px;
		margin: 0 auto;
	}
	h1 {
		text-align: center;
		color: khaki;
		background: #252525;
		padding: 40px;
	}
	ul.todo-list {
		background: #fffce3;
	}
	ul.todo-list.active {
		padding: 16px 0;
	}
	.v-enter-from,
	.v-leave-to {
		opacity: 0;
		transform: translateX(40px);
	}
	.v-enter-active,
	.v-leave-active {
		transition: all 0.4s ease-in-out;
	}
	.v-leave-from,
	.v-enter-to {
		opacity: 1;
		transform: translateX(0px);
	}
</style>
