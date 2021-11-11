<template>
  <header>
    <h1>Vue Todo App</h1>
		<p>Simple todo app built with Vue 3</p>
  </header>
</template>

<script>
export default {
  name: 'TodoHeader',
};
</script>

<style lang="scss" scoped>
	header {
		text-align: center;
		border: 2px solid #34495e;
    margin-bottom: 20px;
		h1 {
			color: #34495e;
		}
		p {
			color: #34495e;
		}
	}
</style>
