<template>
  <div id="app">
    <Slider :slides="slides" />
	<Button @click.native="modalIsOpen=true">К покупкам</Button>
	<Modal :isOpen="modalIsOpen" @toggleModal="modalIsOpen=!modalIsOpen" />
  </div>
</template>

<script>
import Slider from './components/Slider.vue'
import Button from './components/Button.vue'
import Modal from './components/Modal.vue'

export default {
  name: 'App',
  components: {
    Slider,
	Button,
	Modal
  },
  data () {
	return {
		slides: [
			{
				title: 'Привезём точно по списку',
				description: 'Сборщик берëт с собой наручный терминал, на котором он видит весь список покупок для каждого заказа.',
				img: 'slide_1.jpg',
				imgMobile: 'slideMobile_1.jpg'
			},{
				title: 'Собираем быстро и эффективно',
				description: 'Для улучшения эргономики пространства товары размещены от тяжëлых к лëгким, находящимся уже в конечной зоне упаковки.',
				img: 'slide_2.jpg',
				imgMobile: 'slideMobile_2.jpg'
			},{
				title: 'За свежесть и качество отвечаем',
				description: 'Выделены специальные зоны, в том числе холодная и морозильная.',
				img: 'slide_3.jpg',
				imgMobile: 'slideMobile_3.jpg'
			},{
				title: 'Шампунь не положат рядом с рыбой',
				description: 'Собираем и упаковываем ваш заказ с заботой: соблюдаем принципы товарного соседства и учитываем вес товара.',
				img: 'slide_4.jpg',
				imgMobile: 'slideMobile_4.jpg'
			},{
				title: 'Довезëм в сохранности даже яйца',
				description: 'Бережно транспортируем контейнеры, фиксируя их стяжными ремнями. Системы охлаждения поддерживают температурный режим.',
				img: 'slide_5.jpg',
				imgMobile: 'slideMobile_5.jpg'
			}
		],
		modalIsOpen: false
	}
  }
}
</script>

<style>
@font-face {
	font-family: 'RotondaC';
	src: url('~@/assets/fonts/RotondaC_Regular.ttf');
	font-style: normal;
}
body {
	margin: 0;
}
#app {
	min-height: 100vh;
	box-sizing: border-box;
	font-family: 'RotondaC', sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	padding-top: 60px;
	background-color: #E5E5E5;
}
</style>
