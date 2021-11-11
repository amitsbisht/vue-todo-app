<template>
	<form @submit.prevent="addTodo">
		<div class="form-field-wrap">
			<input type="text" name="todo" placeholder="Add Todo here..." v-model="todo" required />
		</div>
		<div class="form-btn-wrap">
			<button type="submit">Add Todo</button>
		</div>
	</form>
</template>

<script>
export default {
  name: 'TodoForm',
  data() {
    return {
      todo: '',
    };
  },
  methods: {
    addTodo() {
      this.$emit('addTodo', this.todo);
      this.todo = '';
    },
  },
};
</script>

<style lang="scss" scoped>
	form {
		display: flex;
    align-items: center;
		.form-field-wrap {
			flex-basis: 70%;
			input {
				width: 100%;
				height: 45px;
				background: transparent;
				border: 2px solid #34495e;
				font-size: 20px;
				line-height: 1;
				padding: 8px 12px;
				font-style: italic;
				&::placeholder {
					color: #34495e;
					font-weight: 600;
				}
			}
		}
		.form-btn-wrap {
			flex-basis: 30%;
			button {
				width: 100%;
				height: 45px;
				border: 2px solid #34495e;
				font-size: 20px;
				line-height: 1;
				font-weight: 600;
				cursor: pointer;
				transition: all .3s ease-in-out;
				&:hover {
					background-color: #4caf50;
					color: #fff;
				}
			}
		}
	}
</style>
