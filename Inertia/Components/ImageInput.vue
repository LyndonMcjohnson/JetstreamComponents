<!-- usage: <image-input @changeImage="this.form.flyer = $event" defaultSrc="/img/illustrations/event-bg.jpg"/> -->

<template>
	<div class="inline-flex relative w-full">
		<label for="image" class="w-full cursor-pointer border bg-blue-100 border-gray-400 rounded-lg overflow-hidden mt-2 border-dashed text-center" :style="'background-image: url(' + src + '); background-size: cover; background-repeat: no-repeat; background-position:center;'">
			<div class="w-full py-16 bg-black bg-opacity-25 hover:bg-opacity-20 text-white">
				<svg class="w-6 h-6 -mt-1 inline-block" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M3 9a2 2 0 012-2h.93a2 2 0 001.664-.89l.812-1.22A2 2 0 0110.07 4h3.86a2 2 0 011.664.89l.812 1.22A2 2 0 0018.07 7H19a2 2 0 012 2v9a2 2 0 01-2 2H5a2 2 0 01-2-2V9z"></path>
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="1" d="M15 13a3 3 0 11-6 0 3 3 0 016 0z"></path>
				</svg>
			</div>
		</label>
		<button v-if="file" @click="remove()" class="absolute top-4 right-2 p-2 text-white bg-gray-300 rounded-full hover:bg-gray-400">
			<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M6 18L18 6M6 6l12 12"></path></svg>
		</button>
		<input id="image" @change="changImage" class="hidden" type="file" accept="image/*" :required="required"/>
		<!-- <img :src="src" class="mt-2 rounded-lg w-full"> -->
	</div>
</template>

<script>
	export default {
		name: 'ImageInput',
		props: {
			required: Boolean,
			defaultSrc: String
		},
		data() {
			return {
				src: this.defaultSrc,
				file: null
			}
		},
		methods: {
			changImage(e) {
				this.file = e.target.files[0]
				this.$emit('changeImage', this.file)
				let reader = new FileReader()
				reader.readAsDataURL(this.file)
				reader.onload = (e) => {
					this.src = e.target.result
				}
			},

			remove() {
				this.src = this.defaultSrc
				this.file = null
				this.$emit('changeImage', this.file)
			}
		}
	}
</script>
