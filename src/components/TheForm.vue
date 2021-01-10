<template>
	<div>
		<form @submit.prevent="addTodo">
			<div class="form-input-wrap">
				<input
					type="text"
					v-model.trim="todo"
					placeholder="For example: Feed dogs..."
					:class="{ 'input-error': error }"
				/>
				<p class="error" v-if="error">Please enter something...</p>
			</div>
			<div class="form-button-wrap">
				<input type="submit" value="Add Todo" />
			</div>
		</form>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				todo: "",
				error: null,
			};
		},
		emits: ["add"],
		methods: {
			addTodo() {
				this.error = null;
				if (this.todo) {
					this.$emit("add", this.todo);
					this.todo = "";
				} else {
					this.error = true;
				}
			},
		},
	};
</script>

<style scoped>
	form {
		display: flex;
	}
	form .form-input-wrap {
		flex: 1;
	}
	form input[type="text"] {
		background: transparent;
		border: 2px solid #ed7a33;
		padding: 8px 10px;
		font-size: 15px;
		width: 100%;
		min-height: 45px;
	}
	form input[type="text"]:focus {
		outline: none;
		box-shadow: 4px 4px 40px 2px rgb(255 249 193);
	}
	form input[type="text"]::placeholder {
		color: #333;
	}
	form input[type="submit"] {
		width: 100%;
		border: 2px solid #ed7a33;
		padding: 0px 20px;
		background: linear-gradient(to right, #f37335, #fdc830);
		color: white;
		min-height: 45px;
		font-weight: 700;
		font-size: 20px;
	}
	form input[type="text"].input-error {
		border-color: #f44336;
	}
	form .error {
		color: #333;
		font-size: 12px;
		font-weight: 700;
		letter-spacing: 0.8px;
	}
</style>
