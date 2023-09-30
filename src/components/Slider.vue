<template>
	<vueper-slides
		:fixedHeight="this.height"
		:bullets="false"
		:lazy="false"
		@ready="init($event)"
      :transitionSpeed="500"
      :infinite="true"
	>
		<vueper-slide
			v-for="(slide, i) in slides"
			:key="i"
		>
			<template #content>
				<div
					class="slider-background"
					:style="{ backgroundImage: `url(${slide.background})` }"
				></div>
				<div class="slide-content"></div>
				<div
					class="slider-foreground"
					:style="{ backgroundImage: `url(${slide.foreground})` }"
				></div>
			</template>
		</vueper-slide>
	</vueper-slides>
</template>

<script>
import { VueperSlides, VueperSlide } from 'vueperslides';
import 'vueperslides/dist/vueperslides.css';

export default {
	name: 'Slider',
	components: { VueperSlides, VueperSlide },
	data: () => ({
		height: '100vh',
		slides: [
			{
				title: 'Slide #1',
				content: 'Slide 1 content.',
				background: '/src/assets/background-1-min.png',
				foreground: '/src/assets/foreground-1-min.png',
            isActive: false
			},
			{
				title: 'Slide #2',
				content: 'Slide 2 content.',
				background: '/src/assets/background-2-min.png',
				foreground: '/src/assets/foreground-2-min.png',
            isActive: false
			},
			{
				title: 'Slide #3',
				content: 'Slide 3 content.',
				background: '/src/assets/background-2-min.png',
				foreground: '/src/assets/foreground-1-min.png',
            isActive: false
			},
		],
	}),
	methods: {
		init(e) {
			console.log(e.currentSlide.index);
         this.slides[e.currentSlide.index].isActive = true
		},
      getClass(position ,slide, i) {
         if (slide.isActive) {
            return `s-${position}-${i}`
         } else {
            return ''
         }
      }
	},
};
</script>

<style scoped>
.vueperslide .slide-content,
.vueperslide .slider-background,
.vueperslide .slider-foreground {
	position: absolute;
	inset: 0;
	background-size: cover;
	transition: all 1000ms ease-in-out;
   transition-delay: 500ms;
}

.slider-foreground {
	opacity: 0;
}

.s-foreground-0 {
   transform: translateX(500px);
}
</style>
