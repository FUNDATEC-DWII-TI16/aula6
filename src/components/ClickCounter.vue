<template>
	<div>
		<button @click="increment()">Click me!</button>
		<div>Total clicks: {{ totalClicks }}</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			totalClicks: 0,
		};
	},
	methods: {
		increment() {
			this.totalClicks++;
		},
	},
};
</script>
