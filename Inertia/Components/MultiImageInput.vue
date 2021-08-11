//requires: Vue3-dropzone @https://www.npmjs.com/package/vue3-dropzone
//Usage: <multi-image-input @getImages="this.form.gallery = $event" />

<template>
	<div>
		<div class="inline-flex w-full relative" v-bind="getRootProps()">
			<input v-bind="getInputProps()" />
			<div v-if="files.length === 0" class="w-full cursor-pointer border border-black rounded-lg overflow-hidden mt-2 border-dashed text-center">
				<div @click="open" class="w-full py-16">
					<p v-if="isDragActive">Drop the files here ...</p>
					<p v-else>Drag & drop some files or click here to upload</p>
				</div>
			</div>	
			<button v-else type="button" @click="open" class="absolute right-2 cursor-pointer text-sm z-30 bottom-2 py-1 px-2 border border-gray-800 rounded-lg">
				Add more images
			</button>
		</div>
		<div ref="images" v-if="files.length > 0" class="mt-2 p-2 relative border border-black rounded-lg border-dashed"></div>
	</div>
</template>

<script>
import { useDropzone } from "vue3-dropzone";
import { ref } from "vue";

export default {
    name: "UseDropzoneDemo",

    emits: ["getImages"],

    setup(props, context) {
        const files = ref([]);
        const images = ref(null);

        const removeImage = (e) => {
            files.value.splice(e.target.getAttribute("data-file"), 1);
            let imageToRemove = e.target.closest(".galleryImage");
            imageToRemove.remove();
            context.emit("getImages", files.value);
        };

        function onDrop(acceptFiles, rejectReasons) {
            files.value.push(...acceptFiles);

            acceptFiles.forEach((file) => {
                let reader = new FileReader();
                reader.readAsDataURL(file);
                reader.onload = (e) => {
                    let div = document.createElement("div");

                    div.setAttribute("class", "rounded-lg inline-block m-2 h-24 overflow-hidden relative galleryImage");
                    div.innerHTML =`<img src="` + e.target.result + `" class="h-full">
						<a data-file="` + files.value.indexOf(file) + `" class="removeImage absolute top-2 right-2 p-1 text-white bg-gray-300 rounded-full cursor-pointer hover:bg-gray-400">
							<svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M6 18L18 6M6 6l12 12"></path></svg>
						</a>`;

                    images.value.appendChild(div);
                    context.emit("getImages", files.value);
                };
            });

            let imageElements = document.getElementsByClassName("removeImage");

            setTimeout(() => {
                for (var i = 0; i < imageElements.length; i++)
                    imageElements[i].addEventListener("click", removeImage);
            }, 1 * 100); //or less

            console.log(rejectReasons);
        }

        const { getRootProps, getInputProps, ...rest } = useDropzone({
            onDrop,
        });

        return {
            getRootProps,
            getInputProps,
            files,
            images,
            removeImage,
            ...rest,
        };
    },
};
</script>
