<template>
	<header class="app-header">
		<a @click="changeGrid" v-if="meshGrid"
			><img src="@/assets/meshGrid.svg" alt="mesh grid"
		/></a>
		<a @click="changeGrid" v-if="!meshGrid"
			><img src="@/assets/hamburgerGrid.svg" alt="hamburger grid"
		/></a>
	</header>
</template>

<script>
export default {
	data() {
		return {
			meshGrid: true
		};
	},
	methods: {
		changeGrid() {
			this.$root.$emit("change-grid");
		}
	},
	mounted() {
		this.$root.$on("grid-value-changed", data => (this.meshGrid = data));
	}
};
</script>

<style lang="scss" scoped>
.app-header {
	height: 50px;
	background-color: #009688;
	display: flex;
	justify-content: flex-end;
	align-items: center;

	a {
		height: 30px;
		width: 30px;
		display: inline-block;
		margin-right: 30px;
		cursor: pointer;
		transition: transform 0.2s ease-in;

		img {
			max-width: 100%;
		}
	}

	a:hover {
		transform: scale(1.08);
	}
}
</style>