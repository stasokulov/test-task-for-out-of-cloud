<template>
	<button class="button" :type="type">
		<slot/>
	</button>
</template>

<script>
export default {
	name: 'Button',
	props: {
		type: {
			type: String,
			default: 'button'
		}
	}
}
</script>

<style scoped>
.button {
	width: 100%;
	max-width: 340px;
	height: 70px;
	box-sizing: border-box;
	padding: 10px;
	left: 550px;
	background: linear-gradient(0deg, #7DB945, #7DB945), #7DB945;
	border-radius: 10px;
	border: none;
	font-family: 'RotondaC', sans-serif;
	font-weight: bold;
	font-size: 22px;
	line-height: 36px;
	text-align: center;
	letter-spacing: 0.01em;
	color: #FFFFFF;
	cursor: pointer;
}
.button:hover {
	box-shadow: 0px 0px 40px rgba(0, 0, 0, 0.1);
}
</style>