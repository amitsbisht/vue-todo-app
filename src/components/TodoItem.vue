<template>
	<li>
		<span class="todo-name" :class="{ completed: todo.isCompleted }">{{
			todo.name
		}}</span>
		<span>
			<img
				id="toggleTodoIcon"
				@click="toggleTodo(todo)"
				class="todo-icon"
				:src="genSvgUrl"
			/>
			<img
				id="removeTodoIcon"
				@click="removeTodo(todo)"
				class="todo-icon"
				:src="removeSvgUrl"
			/>
		</span>
	</li>
</template>

<script>
	export default {
		props: ["todo"],
		computed: {
			genSvgUrl() {
				return this.todo.isCompleted
					? require("../assets/checkbox-checked.svg")
					: require("../assets/checkbox-unchecked.svg");
			},
			removeSvgUrl() {
				return require("../assets/bin.svg");
			},
		},
		emits: ["toggle", "remove"],
		methods: {
			toggleTodo(todo) {
				this.$emit("toggle", todo);
			},
			removeTodo(todo) {
				this.$emit("remove", todo);
			},
		},
	};
</script>

<style scoped>
	li {
		color: #333;
		list-style: none;
		background: #ffee56;
		padding: 12px;
		margin: 0 0 16px 16px;
		font-size: 18px;
		display: flex;
		justify-content: space-between;
		align-items: center;
	}
	.todo-icon {
		padding-right: 5px;
	}
	.todo-icon:last-child {
		padding-right: 0;
	}
	.todo-name.completed {
		text-decoration-line: line-through;
		text-decoration-thickness: 3px;
		font-style: italic;
	}
</style>
