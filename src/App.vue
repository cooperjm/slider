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

.vueperslide {
  transform: translate3d(0,0,0);
  -webkit-transform: translate3d(0, 0, 0);
}

.vueperslides__arrow svg {
	stroke-width: 2px;
}

.vueperslides__arrow svg:hover {
	stroke-width: 2;
}
</style>
