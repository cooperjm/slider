<script>
import Slider from './components/Slider.vue';

export default {
	name: 'App',
	components: { Slider },
};
</script>

<template>
	<slider></slider>
</template>

<style>
body {
	margin: 0;
}

/* .slider-foreground { 
  transition: all 1000ms ease-in-out;
} */

.vueperslide--active .s-foreground-0 {
  transform: translateX(0);
	opacity: 1;
}
/* .vueperslides__track-inner,
.vueperslide,
.vueperslides,
.vueperslides__track {
	perspective: 2000;
	backface-visibility: hidden;
  transform: translate3d(0, 0, 0);
	-webkit-perspective: 2000;
	-webkit-backface-visibility: hidden;
  -webkit-transform: translate3d(0, 0, 0);
} */

.vueperslide {
  transform: translate3d(0,0,0);
  -webkit-transform: translate3d(0, 0, 0);
}
</style>
