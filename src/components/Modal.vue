<template>
<div v-if="isOpen" class="modal">
	<div class="modal-inner">
		<div @click="$emit('toggleModal')" class="close-btn"></div>
		<form v-if="!emailIsSend" @submit.prevent="" class="form">
			<p v-if="validateEmailFailed" class="error-message">Email не верного формата</p>
			<input v-model="email" type="email" class="input" :class="{'error-input': validateEmailFailed}" placeholder="E-mail">
			<Button @click.native="validateEmail" type="submit">Отправить</Button>
		</form>
		<div v-if="emailIsSend && answerReceived" class="thanks">
			<p>Спасибо!</p>
			<Button @click.native="emailIsSend=false">Еще отправить</Button>
		</div>
		<div v-if="emailIsSend && !answerReceived" class="preloader">
			Ожидайте
		</div>
	</div>
</div>
</template>

<script>
import Button from './Button.vue'

export default {
	name: 'Modal',
	components: {
		Button
	},
	props: {
		isOpen: {
			type: Boolean,
			default: false
		}
	},
	data() {
		return {
			email: '',
			validateEmailFailed: false,
			emailIsSend: false,
			answerReceived: false
		}
	},
	methods: {
		sendEmail() {
			// Выводим email в консоль согласно условиям задания
			console.log(this.email);
			this.emailIsSend = true;
			this.answerReceived = false;

			// Имитация отправки формы на сервер
			fetch('https://jsonplaceholder.typicode.com/todos/1')  // Реальный запрос на сервер
			.then(response => response.json())
			.then(json => {
					console.log(json);
					// Добавим секудну, чтобы было не слишком быстро
					setTimeout(() => {
						this.answerReceived = true;
					}, 1000)
				})
		},
		validateEmail() {
			const regexp = /^([A-Za-z0-9_\-.])+@([A-Za-z0-9_\-.])+\.([A-Za-z]{2,4})$/;
			if( regexp.test(this.email) ) {
				this.validateEmailFailed = false;
				this.sendEmail();
			} else {
				this.validateEmailFailed = true;
			}			
		}
	}
}
</script>

<style scoped>
.modal {
	display: flex;
	position: fixed;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	justify-content: center;
	align-items: center;
	background-color: rgba(0, 0, 0, .5);
}
.modal-inner {
	position: relative;
	display: flex;
	justify-content: center;
	align-items: center;
	width: 300px;
	height: 200px;
	padding: 20px;
	box-sizing: border-box;
	background-color: #ddd;
	border-radius: 5px;
}
.close-btn {
	position: absolute;
	top: 10px;
	right: 10px;
	height: 15px;
	width: 15px;
	background-image: url("data:image/svg+xml,%3Csvg height='311pt' viewBox='0 0 311 311.1' width='311pt' xmlns='http://www.w3.org/2000/svg'%3E%3Cpath d='M16 311c-4 0-8-1-11-5-7-6-7-16 0-22L284 5a16 16 0 1122 22L27 306c-3 3-7 5-11 5zm0 0'/%3E%3Cpath d='M295 311c-4 0-8-1-11-5L5 27A16 16 0 0127 5l279 279a16 16 0 01-11 27zm0 0'/%3E%3C/svg%3E");
	background-position: center;
	background-repeat: no-repeat;
	background-size: contain;
	cursor: pointer;
}
.form {
	position: relative;
	display: flex;
	flex-direction: column;
	width: 100%;
}
.error-message {
	position: absolute;
	top: -15px;
	left: 0;
	text-align: left;
    font-size: 10px;
    color: #f00;
    margin: 0;
}
.input {
	padding: 10px;
	margin-bottom: 20px;
	border: none;
}
.error-input {
	box-shadow: 0 0 8px 0 #f00;
}
.thanks {
	font-weight: bold;
	font-size: 22px;
	line-height: 36px;
	text-align: center;
}
.preloader {
	animation: 4s linear 0s infinite normal preloader;
}
@keyframes preloader {
	from { transform: rotate(0deg); }
	to { transform: rotate(360deg); }
}
</style>