<template>
	<div>
		<ul>
			<li v-for="(todo, index) in todos" :key="index" :class="{ completed: todo.isCompleted }">
				<span class="todo-value" @dblclick="$emit('toggleTodo', index)">{{ todo.value }}</span>
				<span class="todo-remove" @click="removeTodo($event, index)" title="Remove Todo"></span>
			</li>
		</ul>
	</div>
</template>

<script>
export default {
  name: 'TodoList',
  props: {
    todos: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      removing: false,
    };
  },
  methods: {
    removeTodo($event, index) {
      if (this.removing) return;
      $event.target.parentElement.classList.add('removing');
      this.removing = true;
      setTimeout(() => {
        $event.target.parentElement.classList.remove('removing');
        this.$emit('removeTodo', index);
        this.removing = false;
      }, 750);
    },
  },
};
</script>

<style lang="scss" scoped>
	ul {
		list-style: none;
    max-height: 250px;
    overflow-y: auto;
		margin: 0;
		padding-left: 20px;
		li {
			position: relative;
			font-size: 20px;
			font-weight: 600;
			margin: 15px 0;
			display: flex;
			justify-content: space-between;
			transition: all .3s ease-in-out;
			&.removing {
				animation: remove 1s infinite;
			}
			&.completed {
				.todo-value {
					text-decoration: line-through;
					&::before {
						background-color: #ffffff;
						border-width: 6px;
						border-color: #34495e;
					}
				}
			}
			.todo-value {
				cursor: pointer;
				max-width: 80%;
				overflow: hidden;
				text-overflow: ellipsis;
				display: -webkit-box;
				-webkit-line-clamp: 2;
				line-clamp: 2;
				-webkit-box-orient: vertical;
				padding-left: 25px;
				font-weight: 600;
				color: #34495e;
				&::before {
					content: '';
					width: 20px;
					height: 20px;
					background: transparent;
					border: 2px solid;
					border-radius: 50px;
					position: absolute;
					top: 50%;
					left: 0;
					transform: translateY(-50%);
					transition: all .3s ease-in-out;
				}
				&:hover {
					&::before {
						background-color: #ffffff;
						border-width: 6px;
						border-color: #34495e;
					}
				}
			}
			.todo-remove {
				cursor: pointer;
				color: #34495e;
				&::after {
					content: '\2718';
					position: absolute;
					top: 50%;
					right: 20px;
					transform: translateY(-50%);
				}
			}
		}
	}

	@keyframes remove {
		0% {
			transform: translateX(0);
		}
		100% {
			transform: translateX(-120%);
			opacity: 0;
			visibility: hidden;
		}
	}
</style>
