<template>
	<div class="bg-white mb-8 border rounded-lg">
		<div class="px-4 py-2">
			<div class="inline-flex items-center items-top">
				<button class="inline-block text-sm border-2 border-transparent rounded-full focus:outline-none transition">
					<img class="h-8 w-8 rounded-full object-cover" :src="media.user.profile_photo_url" :alt="media.user.name" />
				</button>
				<span class="font-black text-sm ml-2">
					{{media.user.name}}
				</span>
			</div>
			<a href="#" class="float-right mt-2 text-gray-400">
				<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 12h.01M12 12h.01M19 12h.01M6 12a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0zm7 0a1 1 0 11-2 0 1 1 0 012 0z"></path></svg>
			</a>
		</div>
		<img :src="media.image" class="w-full" alt="{{media.title}}">
		<div class="py-2 px-4">
			<inertia-link :href="'#'" class="mr-2 text-gray-300">
				<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 inline-block" viewBox="0 0 20 20" fill="currentColor">
					<path d="M5 4a2 2 0 012-2h6a2 2 0 012 2v14l-5-2.5L5 18V4z" />
				</svg>
			</inertia-link>
			<inertia-link :href="'#'" class="mr-2 text-gray-300">
				<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 inline-block" viewBox="0 0 20 20" fill="currentColor">
					<path d="M2 5a2 2 0 012-2h7a2 2 0 012 2v4a2 2 0 01-2 2H9l-3 3v-3H4a2 2 0 01-2-2V5z" />
					<path d="M15 7v2a4 4 0 01-4 4H9.828l-1.766 1.767c.28.149.599.233.938.233h2l3 3v-3h2a2 2 0 002-2V9a2 2 0 00-2-2h-1z" />
				</svg>
			</inertia-link>
			<inertia-link :href="'#'" class="text-gray-300">
				<svg class="w-5 h-5 inline-block" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
					<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-8l-4-4m0 0L8 8m4-4v12"></path>
				</svg>
			</inertia-link>
			<inertia-link :href="'#'" class="float-right text-green-500">
				<svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 inline-block" viewBox="0 0 20 20" fill="currentColor">
					<path d="M2 6a2 2 0 012-2h12a2 2 0 012 2v2a2 2 0 100 4v2a2 2 0 01-2 2H4a2 2 0 01-2-2v-2a2 2 0 100-4V6z" />
				</svg>
			</inertia-link>
		</div>
		<div class="py-2 px-4 text-sm">
			{{media.title}} &middot; <span class="text-gray-400">{{media.other_info}}</span>
			<p>
				<a :href="'#'">
					{{media.other_info}}
				</a>
			</p>
			<p class="text-gray-500 my-2">
				{{media.other_info}} &middot; {{media.other_info}}
			</p>
			<p class="my-2">
				{{media.other_info}}
			</p>
		</div>
	</div>
</template>

<script>
	export default {
		name: 'MediaCard',

		props: {
			media: Object
		}
	}
</script>
