<template>
	<div class="slider-container">
		<vueper-slides
			:fixed-height="this.height"
			:bullets="false"
			:lazy="false"
			@ready="init($event)"
			@slide="setActive($event)"
			:transitionSpeed="600"
			:infinite="true"
			:gap="0"
			@previous="test($event, 'previous')"
			@next="test($event, 'next')"
		>
			<vueper-slide
				v-for="(slide, i) in slides"
				:key="i"
			>
				<template #content>
					<div
						class="slider-background-container"
						:class="getClass('background', slide, i)"
						:style="{ backgroundImage: `url(${slide.background})` }"
					></div>
					<div class="slider-content-container">
						<div
							class="slider-content"
							:class="getClass('content', slide, i)"
						>
							<h2>{{ slide.content }}</h2>
						</div>
					</div>
					<div class="slider-foreground-container">
						<div
							class="slider-foreground"
							:class="getClass('foreground', slide, i)"
							:style="{ backgroundImage: `url(${slide.foreground})` }"
						></div>
					</div>
				</template>
			</vueper-slide>
		</vueper-slides>
	</div>
</template>

<script>
import { VueperSlides, VueperSlide } from 'vueperslides';
import 'vueperslides/dist/vueperslides.css';
import bg1 from '../assets/background-1-min.png';
import fg1 from '../assets/foreground-1-min.png';
import bg2 from '../assets/background-2-min.png';
import fg2 from '../assets/foreground-2-min.png';



export default {
	name: 'Slider',
	components: { VueperSlides, VueperSlide },
	data: () => ({
		height: '90vh',
		slides: [
			{
				title: 'Slide #1',
				content: 'CONNECTING HEAD HEART HAND',
				background: bg1,
				foreground: fg1,
				isActive: false,
			},
			{
				title: 'Slide #2',
				content: 'Slide 2 content.',
				background: bg2,
				foreground: fg1,
				isActive: false,
			},
			{
				title: 'Slide #3',
				content: 'Slide 3 content.',
				background: bg2,
				foreground: fg1,
				isActive: false,
			},
		],
	}),
	methods: {
		init(e) {
			setTimeout(() => {
				this.slides[e.currentSlide.index].isActive = true;
			}, 500);
		},
		getClass(position, slide, i) {
			return slide.isActive ? `s-${position}-${i} c-${i}` : `c-${i}`;
		},
		setActive(e) {
			let currentIndex = e.currentSlide.index;

			this.slides.forEach((slide, index, arr) => {
				if (index === currentIndex) {
					arr[index].isActive = true;
				} else {
					arr[index].isActive = false;
				}
			});
		},
		test(e, msg) {
			console.log(`${msg}`, e);
		},
	},
};
</script>

<style scoped>

.vueperslides__arrow svg {
	stroke-width: 2px;
}

/* .slider-container {
	max-height: 80vh;
	
} */
.vueperslides {
	--delay: 0ms;
}
.vueperslide {
	overflow: hidden;
}


.slider-foreground,
.slider-content,
.slider-background,
.vueperslide .slider-content-container,
.vueperslide .slider-background-container,
.vueperslide .slider-foreground-container {
	position: absolute;
	inset: 0;
	background-size: cover;
	background-repeat: no-repeat;
	/* transition: all 1000ms ease-in-out; */
	transition-delay: var(--delay);
	overflow: hidden !important;
}

.slider-foreground {
	/* opacity: 0; */
	width: 100%;
	height: 100%;
	transition: all 1500ms cubic-bezier(0.45, 0.05, 0.55, 0.95);
	transition-delay: var(--delay);
	overflow: hidden !important;
	transform: translateX(100%);
}

.slider-content {
	opacity: 0;
	display: flex;
	align-items: center;
	width: 100%;
	height: 100%;
	transition: all 1500ms cubic-bezier(0.45, 0.05, 0.55, 0.95);
	transition-delay: var(--delay);
	overflow: hidden !important;
	transform: translateX(-25%);
}

.vueperslide--visible .s-foreground-0 {
	opacity: 1;
	transform: translateX(0);
}

.vueperslide--visible .s-content-0 {
	opacity: 1;
	transform: translateX(15%);
}

.vueperslide--visible .s-foreground-0 {
	opacity: 1;
}
.s-content-0 {
	opacity: 1;
	/* transform: translateX(15%); */
}

.c-0 h2 {
	width: 5ch;
	color: white;
	font-size: clamp(2rem, -1.5rem + 8vw, 6rem);
}
</style>
