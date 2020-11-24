<template>
	<div>
		<div class="flex flex-col h-screen items-center justify-center">
			<h3 class="m-5 text-5xl">{{ state }}</h3>
			<h3 class="m-5 text-7xl">{{ convertToTime(clock) }}</h3>
			<div class="flex justify-center mt-5">
				<button
					v-on:click="handlePlayPause"
					class="text-grey-darkest font-bold py-2 px-4 rounded inline-flex items-center focus:outline-none"
				>
					<svg
						v-if="!playing"
						class="w-16 h-16 m-1"
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke="currentColor"
					>
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M14.752 11.168l-3.197-2.132A1 1 0 0010 9.87v4.263a1 1 0 001.555.832l3.197-2.132a1 1 0 000-1.664z"
						/>
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
						/>
					</svg>
					<svg
						v-else
						class="w-16 h-16 m-1"
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke="currentColor"
					>
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M10 9v6m4-6v6m7-3a9 9 0 11-18 0 9 9 0 0118 0z"
						/>
					</svg>
				</button>
				<button
					v-on:click="handleReset"
					class="text-grey-darkest font-bold py-2 px-4 rounded inline-flex items-center focus:outline-none"
				>
					<svg
						class="w-16 h-16 m-1"
						xmlns="http://www.w3.org/2000/svg"
						fill="none"
						viewBox="0 0 24 24"
						stroke="currentColor"
					>
						<path
							stroke-linecap="round"
							stroke-linejoin="round"
							stroke-width="2"
							d="M4 4v5h.582m15.356 2A8.001 8.001 0 004.582 9m0 0H9m11 11v-5h-.581m0 0a8.003 8.003 0 01-15.357-2m15.357 2H15"
						/>
					</svg>
				</button>
			</div>
		</div>

		<Navbar>
			<div class="flex flex-col items-center justify-center h-screen">
				<div class="custom-number-input h-10 w-48 m-12">
					<label for="custom-input-number" class="w-full text-gray-700 text-2xl font-semibold">Session Length
					</label>
					<div class="flex flex-row h-10 w-full rounded-lg relative bg-transparent mt-2">
						<button v-on:click="sessionDecrease" :disabled="playing" class=" bg-gray-300 text-gray-600 hover:text-gray-700 hover:bg-gray-400 h-full w-20 rounded-l cursor-pointer outline-none">
							<span class="m-auto text-5xl font-thin">−</span>
						</button>
						<input type="number" :disabled="playing" min="1" class="focus:outline-none text-center w-full bg-gray-300 font-semibold text-xl hover:text-black focus:text-black  md:text-basecursor-default flex items-center text-gray-700  outline-none" name="custom-input-number" v-model.number="session" @change="sessionChange"/>
						<button v-on:click="sessionIncrease" :disabled="playing" class="bg-gray-300 text-gray-600 hover:text-gray-700 hover:bg-gray-400 h-full w-20 rounded-r cursor-pointer">
							<span class="m-auto text-5xl font-thin">+</span>
						</button>
					</div>
				</div>
				<hr/>
				<div class="custom-number-input h-10 w-48 m-12">
					<label for="custom-input-number" class="w-full text-gray-700 text-2xl font-semibold">Short hreak Length
					</label>
					<div class="flex flex-row h-10 w-full rounded-lg relative bg-transparent mt-1">
						<button v-on:click="shortDecrease" :disabled="playing" class=" bg-gray-300 text-gray-600 hover:text-gray-700 hover:bg-gray-400 h-full w-20 rounded-l cursor-pointer outline-none">
							<span class="m-auto text-5xl font-thin">−</span>
						</button>
						<input type="number" :disabled="playing" min="1" class="focus:outline-none text-center w-full bg-gray-300 font-semibold text-xl hover:text-black focus:text-black  md:text-basecursor-default flex items-center text-gray-700 " name="custom-input-number" v-model.number="short" @change="shortChange"/>
						<button v-on:click="shortIncrease" :disabled="playing" class="bg-gray-300 text-gray-600 hover:text-gray-700 hover:bg-gray-400 h-full w-20 rounded-r cursor-pointer">
							<span class="m-auto text-5xl font-thin">+</span>
						</button>
					</div>
				</div>
				<hr/>
				<div class="custom-number-input h-10 w-48 m-12">
					<label for="custom-input-number" class="w-full text-gray-700 text-2xl font-semibold">Long Break Length
					</label>
					<div class="flex flex-row h-10 w-full rounded-lg relative bg-transparent mt-1">
						<button v-on:click="longDecrease" :disabled="playing" class=" bg-gray-300 text-gray-600 hover:text-gray-700 hover:bg-gray-400 h-full w-20 rounded-l cursor-pointer outline-none">
							<span class="m-auto text-5xl font-thin">−</span>
						</button>
						<input type="number" :disabled="playing" min="1" class="focus:outline-none text-center w-full bg-gray-300 font-semibold text-xl hover:text-black focus:text-black  md:text-basecursor-default flex items-center text-gray-700  outline-none" name="custom-input-number" v-model.number="long" @change="longChange"/>
						<button v-on:click="longIncrease" :disabled="playing" class="bg-gray-300 text-gray-600 hover:text-gray-700 hover:bg-gray-400 h-full w-20 rounded-r cursor-pointer">
							<span class="m-auto text-5xl font-thin">+</span>
						</button>
					</div>
				</div>
			</div>
		</Navbar>
	</div>
</template>

<style>
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
	-webkit-appearance: none;
	margin: 0;
}

.custom-number-input input:focus {
	outline: none !important;
}

.custom-number-input button:focus {
	outline: none !important;
}
</style>


<script>
	import Navbar from "@/components/Navbar.vue";

	export default {
		name: "Counter",
		components: {
			Navbar
		},
		data: () => ({
			session: 25,
			short: 5,
			long: 20,
			workCounter: 0,
			clock: 25 * 60,
			loop: undefined,
			playing: false,
			state: "Session",
		}),
		methods: {
			convertToTime(count) {
				const minutes = Math.floor(count / 60);
				let seconds = count % 60;
				seconds = seconds < 10 ? "0" + seconds : seconds;

				return `${minutes}:${seconds}`;
			},
			handlePlayPause() {
				if (this.playing) {
					clearInterval(this.loop);
					this.playing = false;
				} else {
					this.playing = true;
					this.loop = setInterval(() => {
						if (this.clock === 0) {
							switch (this.state) {
								case "Session":
									this.workCounter = this.workCounter + 1;
									this.state = "Break";
									if (this.workCounter == 4) {
										this.clock = this.long * 60;
										this.workCounter = 0;
									} else {
										this.clock = this.short * 60;
									}
									break;
								case "Break":
									this.state = "Session";
									this.clock = this.session * 60;
									break;
							}
						} else {
							this.clock = this.clock - 1;
						}
					}, 1000);
				}
			},
			handleReset() {
				clearInterval(this.loop);
				this.clock = this.session * 60;
				this.state = "Session";
				this.playing = false;
				this.workCounter = 0;
			},
			sessionDecrease() {
				if (this.session > 1) {
					this.session = this.session - 1;
					if (this.state == "Session") {
						this.clock = this.session * 60
					}
				}
			},
			sessionIncrease() {
				this.session = this.session + 1;
				if (this.state == "Session") {
					this.clock = this.session * 60
				}
			},
			sessionChange() {
				if (this.state == "Session") {
					this.clock = this.session * 60
				}
			},
			shortDecrease() {
				if (this.short > 1) {
					this.short = this.short - 1;
				}
			},
			shortIncrease() {
				this.short = this.short + 1;
			},
			shortChange() {
				this.clock = this.short * 60
			},
			longDecrease() {
				if (this.long > 1) {
					this.long = this.long - 1;
				}
			},
			longIncrease() {
				this.long = this.long + 1;
			},
			longChange() {
				this.clock = this.long * 60
			},
		},
	};
</script>
