<template lang="html">

	<div :class="element"></div>

</template>

<script lang="js">

	export default {
		name: 'comparisonImageSlider',
		props: {
			element: {
				type: String,
				required: true
			},
			imageLeft: {
				type: String,
				required: true
			},
			imageRight: {
				type: String,
				required: true
			}
			},
		data() {
			return {

			}
		},
		methods: {
			insertExternalSource: function(){
				function comparisonImagesSlider(elements, leftImage, rightImage) {

					var x,
					i;

					document.querySelector(elements).innerHTML = '<div class="comparison__image__container"><div class="comparison__image__img"><img src="' + rightImage + '"/></div><div class="comparison__image__img comparison__image__overlay"><img src="' + leftImage + '"/></div></div>';

					function compareImages(img, classElement) {

						var slider,
							toggleClick = 0,
							w,
							h;

						w = img.offsetWidth;
						h = img.offsetHeight;

						img.style.width = (w / 2) + "px";

						slider = document.createElement("DIV");
						slider.setAttribute("class", classElement);

						img.parentElement.insertBefore(slider, img);

						slider.style.top = (h / 2) - (slider.offsetHeight / 2) + "px";
						slider.style.left = (w / 2) - (slider.offsetWidth / 2) + "px";

						slider.addEventListener("mousedown", sliderReady);

						window.addEventListener("mouseup", sliderFinish);

						slider.addEventListener("touchstart", sliderReady);

						window.addEventListener("touchstop", sliderFinish);

						function sliderReady(e) {

							e.preventDefault();

							toggleClick = 1;

							window.addEventListener("mousemove", sliderMoving);
							window.addEventListener("touchmove", sliderMoving);

						}

						function sliderFinish() {

							toggleClick = 0;

						}

						function sliderMoving(e) {

							var pos;

							if (toggleClick === 0) return false;

							pos = getCursorPosition(e)

							if (pos < 0) pos = 0;
							if (pos > w) pos = w;

							sliderPosition(pos);

						}

						function getCursorPosition(e) {

							var a,
								x = 0;

							e = e || window.event;

							a = img.getBoundingClientRect();

							x = e.pageX - a.left;

							x = x - window.pageXOffset;

							return x;

						}

						function sliderPosition(x) {

							img.style.width = x + "px";

							slider.style.left = img.offsetWidth - (slider.offsetWidth / 2) + "px";

						}

					}

					x = document.querySelectorAll(".comparison__image__overlay");

					for (i = 0; i < x.length; i++) {

						compareImages(x[i], "comparison__image__slider");

					}

				}

				comparisonImagesSlider("." + this.element, this.imageLeft, this.imageRight);
			}
		},
		mounted() {
			this.insertExternalSource();
		},
		computed: {

		}
}

</script>

<style>
* {
	box-sizing: border-box;
}

.comparison__image__container {
	position: relative;
	height: 200px;
}

.comparison__image__img {
	position: absolute;
	width: auto;
	height: auto;
	overflow: hidden;
}

.comparison__image__img img {
	display: block;
	vertical-align: middle;
}

.comparison__image__slider {
	position: absolute;
	z-index: 9;
	cursor: ew-resize;
	width: 25px;
	height: 25px;
	background-color: rgba(41, 124, 192, 0.616);
	opacity: 0.7;
	border-radius: 50%;
}

img {
	width: 300px;
	height: 200px;
}
</style>
