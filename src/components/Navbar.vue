<template>
	<div>
		<!-- Sidebar -->
		<aside
			:class="isOpen ? 'block' : 'hidden'"
			class="top-0 right-0 z-30 fixed w-full h-full bg-white"
		>
			<div class="bg-gray-800 shadow-xs md:block">
				<slot></slot>
			</div>
		</aside>

		<!-- Header -->
		<span
			class="text-xl block hover:border-gray-500 cursor-pointer top-0 right-0 p-5 z-50 fixed"
			@click.prevent="isOpen = !isOpen"
		>
			<svg
				v-if="!isOpen"
				class="w-10 h-10 z-30"
				xmlns="http://www.w3.org/2000/svg"
				fill="none"
				viewBox="0 0 24 24"
				stroke="currentColor"
			>
				<path
					stroke-linecap="round"
					stroke-linejoin="round"
					stroke-width="2"
					d="M4 6h16M4 12h16M4 18h16"
				/>
			</svg>

			<svg
				v-else
				class="w-10 h-10 z-30"
				xmlns="http://www.w3.org/2000/svg"
				fill="none"
				viewBox="0 0 24 24"
				stroke="currentColor"
			>
				<path
					stroke-linecap="round"
					stroke-linejoin="round"
					stroke-width="2"
					d="M6 18L18 6M6 6l12 12"
				/>
			</svg>
		</span>
	</div>
</template>

<script>
	export default {
		data: () => ({
			isOpen: false,
		}),
	}
</script>
