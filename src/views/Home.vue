<template>
	<div class="home">
		<img alt="Vue logo" src="../assets/logo.png">
		<HelloWorld msg="Welcome to Your Vue.js App"/>
		<comparisonImageSlider
			element="imageComparison"
			imageRight="https://images.pexels.com/photos/417173/pexels-photo-417173.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500"
			imageLeft="https://www.themayor.eu/uploads/image/file/2490/medium_forest.jpg?1552485595"
		/>
	</div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import comparisonImageSlider from '@/components/comparisonImageSlider.vue'

export default {
	name: 'home',
	components: {
		HelloWorld,
		comparisonImageSlider,
	}
}
</script>
