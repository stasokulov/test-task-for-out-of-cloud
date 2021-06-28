<template>
	<div class="slider-wrapper">
		<div class="slider">
			<ul class="slider-list">
				<li v-for="(slide, index) in computedSlides"
					:key="index"
					class="slide"
					:class="{active: slide.isActive}"
				>
					<div class="slide-number">{{index+1}}</div>
					<picture>
						<source :srcset="slide.imgMobile" media="(max-width: 1024px)">
						<img :alt="slide.title" :src="slide.img" class="img">
					</picture>		
					<p class="title"><b>{{slide.title}}</b></p>
					<p class="description">{{slide.description}}</p>
				</li>
			</ul>
			<div @click="changeSlide('prev')" class="arrow arrow-left"></div>
			<div @click="changeSlide('next')" class="arrow arrow-right"></div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Slider',
	data() {
		return {
			activeSlide: 0
		}
	},
	props: {
		slides: Array
	},
	computed: {
		computedSlides: function() {
			const computedSlides = [];
			const path = './img/';
			this.slides.forEach(slide => {
				if (!slide.img.includes(path)) {
					slide.img = `${path}${slide.img}`;
				}
				if (!slide.imgMobile.includes(path)) {
					slide.imgMobile = `${path}${slide.imgMobile}`;
				}
				slide.isActive = false;
				computedSlides.push(slide);
			});
			computedSlides[this.activeSlide].isActive = true;
			return computedSlides;
		}
	},
	methods: {
		changeSlide(what) {
			if(what === 'next') {
				this.activeSlide === this.computedSlides.length - 1 ?
				this.activeSlide = 0 :
				this.activeSlide++
			}
			if(what === 'prev') {
				this.activeSlide === 0 ?
				this.activeSlide = this.computedSlides.length - 1 :
				this.activeSlide--
			}
		}
	}
}
</script>

<style scoped>
.slider-wrapper {
	display: flex;
	justify-content: center;
	margin-bottom: 50px;
}
.slider {
	position: relative;
	width: 640px;
	height: 450px;
	font-family: 'RotondaC', sans-serif;
	font-style: normal;
}
.slider-list {
	position: relative;
	width: 100%;
	height: 100%;
	margin: 0;
	padding: 0;
	list-style: none;
}
.slide {
	position: absolute;
	top: 50%;
	left: 50%;
	transform: translate(-50%, -50%);
	width: 100%;
	height: 100%;
	box-sizing: border-box;
	opacity: 0;
	background-color: #fff;
	padding: 40px;
	transition: opacity, 1s;
	box-shadow: 0px 0px 40px rgba(0, 0, 0, 0.1);
	border-radius: 10px;
}
.active {
	opacity: 1;
}
.slide-number {
	display: flex;
	position: absolute;
	width: 50px;
	height: 50px;
	top: 28px;
	left: 36px;
	justify-content: center;
	align-items: center;
	border-radius: 50%;
	background: #fff;
	font-weight: bold;
	font-size: 22px;
	line-height: 46px;
	text-align: center;
	color: #7DB945;
}
.img {
	display: block;
	width: 100%;
	height: auto;
	margin-bottom: 28px;
}
.title {
	margin: 0;
	font-size: 16px;
	line-height: 24px;
	text-align: center;
	color: #26303B;
}
.description {
	margin: 0;
	font-size: 16px;
	line-height: 24px;
	text-align: center;
	color: #26303B
}
.arrow {
	position: absolute;
	top: 50%;
	width: 20px;
	height: 40px;
	transform: translate(0, -50%);
	cursor: pointer;
}
.arrow:before {
	content: '';
	position: absolute;
	top: 0;
	bottom: 0;
	left: 0;
	right: 0;
	background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='44' fill='none'%3E%3Cpath d='M2 2l20 20L2 42' stroke='%23D0D5CD' stroke-width='3' stroke-linecap='round' stroke-linejoin='round'/%3E%3C/svg%3E");
	background-repeat: no-repeat;
	background-position: center;
	background-size: contain;
}
.arrow-left {
	right: calc(100% + 30px);
}
.arrow-left::before {
	transform: rotate(-180deg);
}
.arrow-right {
	left: calc(100% + 30px);
}

@media (max-width: 1024px) {
	.slider {
		width: 280px;
		height: 350px;
		padding-bottom: 62px;
	}
	.slide {
		padding: 20px;
	}
	.slide-number {
		top: 11px;
		left: 12px;
		width: 40px;
		height: 40px;
		font-size: 16px;
	}
	.img {
		margin-bottom: 20px;
	}
	.title {
		font-size: 14px;
		line-height: 22px;
	}
	.description {
		font-size: 14px;
		line-height: 22px;
	}
	.arrow {
		top: auto;
		bottom: 0;
		transform: none;
		width: 14px;
		height: 28px;
	}
	.arrow-left {
		right: auto;
		left: calc(50% - 30px - 14px);
	}
	.arrow-right {
		right: calc(50% - 30px - 14px);
		left: auto;
	}
}
</style>
