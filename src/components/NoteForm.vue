<template>
	<form class="form">
		<input
			type="text"
			v-model="inputHeader"
			ref="headerInput"
			class="input-header"
			placeholder="Napíšte názov..."
		/>
		<small>Napíšte poznámku</small>
		<input v-model="inputText" class="input-text" />
		<div class="submit">
			<button @click.prevent="addNote">Pridať</button>
		</div>
	</form>
</template>

<script>
export default {
	data() {
		return {
			inputHeader: "",
			inputText: ""
		};
	},
	methods: {
		addNote() {
			if (!this.inputHeader || !this.inputText) return;
			const newNote = {
				header: this.inputHeader,
				text: this.inputText,
				timestamp: new Date().toLocaleString(),
				edit: false
			};

			this.$root.$emit("add-note", newNote);
			this.inputHeader = "";
			this.inputText = "";
			this.$refs.headerInput.focus();
		}
	},
	mounted() {
		this.$refs.headerInput.focus();
	}
};
</script>

<style lang="scss" scoped>
.form {
	width: 30%;
	display: flex;
	flex-flow: column;
	box-shadow: 0 3px 6px rgba(0, 0, 0, 0.1), 0 3px 6px rgba(0, 0, 0, 0.05);
	margin: 2em auto 0;
	min-height: 50px;
	padding: 0.5em;

	input {
		background: none;
		border: none;
		outline: none;
	}

	small {
		font-size: 0.7em;
		text-align: left;
		color: rgba(0, 0, 0, 0.65);
	}

	.input-header {
		margin: 0.5em 0 1em 0;
	}

	.input-text {
		border-bottom: 1px solid #009688;
		padding: 0.15em 0;
	}
	.submit {
		display: flex;
		justify-content: flex-end;

		button {
			width: 70px;
			background: #009688;
			border: none;
			margin-top: 0.6em;
			padding: 0.4em;
			color: #eee;
			text-transform: uppercase;
			letter-spacing: 0.5px;
			cursor: pointer;
		}
	}
}
</style>