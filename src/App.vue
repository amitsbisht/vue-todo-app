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
						v-for="todo in todos"
						:key="todo.id"
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
	import axios from "axios";

	export default {
		name: "App",
		components: {
			TheForm,
			TodoItem,
		},
		data() {
			return {
				todos: [],
				todoUrl: process.env.VUE_APP_TODO_REST_URL,
				todoPathUrl: process.env.VUE_APP_TODO_PATH_URL,
			};
		},
		mounted() {
			axios
				.get(`${this.todoUrl}`)
				.then((res) => {
					const data = res.data;
					for (const id in data) {
						const todo = {
							id: id,
							name: data[id].name,
							isCompleted: data[id].isCompleted,
						};
						this.todos.push(todo);
					}
				})
				.catch((error) => console.log(error));
		},
		methods: {
			addTodo(todo) {
				const newTodo = {
					name: todo,
					isCompleted: false,
				};
				axios
					.post(`${this.todoUrl}`, {
						name: newTodo.name,
						isCompleted: newTodo.isCompleted,
					})
					.then((response) => {
						newTodo.id = response.data.name;
						this.todos.push(newTodo);
					})
					.catch(function(error) {
						console.log(error);
					});
			},
			toggleTodo(todo) {
				axios
					.patch(`${this.todoPathUrl}${todo.id}.json`, {
						isCompleted: !todo.isCompleted,
					})
					.then((res) => {
						todo.isCompleted = !todo.isCompleted;
					})
					.catch((error) => console.log(error));
			},
			removeTodo(removeTodo) {
				axios
					.delete(`${this.todoPathUrl}${removeTodo.id}.json`)
					.then((res) => console.log(res))
					.catch((error) => console.log(error));
				const removeTodoIndex = this.todos.findIndex(
					(todo) => todo.id == removeTodo.id
				);
				this.todos.splice(removeTodoIndex, 1);
			},
		},
	};
</script>

<style>
	@import url("https://fonts.googleapis.com/css2?family=Titillium+Web:ital,wght@0,200;0,400;0,700;1,700&display=swap");
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
		font-family: "Titillium Web", sans-serif;
	}
	#app {
		max-width: 450px;
		margin: 0 auto;
	}
	#app main {
		background: #fffce3;
	}
	h1 {
		text-align: center;
		color: #fff;
		padding: 40px;
		background: linear-gradient(to right, #f37335, #fdc830);
		font-weight: 700;
		font-style: italic;
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
