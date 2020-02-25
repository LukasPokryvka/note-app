<template>
	<div id="app">
		<Header />
		<NoteForm />
		<NoteList />
	</div>
</template>

<script>
import Header from "@/components/Header.vue";
import NoteForm from "@/components/NoteForm.vue";
import NoteList from "@/components/NoteList.vue";

export default {
	name: "app",
	components: {
		NoteForm,
		NoteList,
		Header
	}
};
</script>

<style lang="scss">
@import "./assets/css/reset";
@import url("https://fonts.googleapis.com/css?family=Caveat:400,700&display=swap&subset=latin-ext");

* {
	box-sizing: border-box;
}

textarea {
	resize: none;
}

#app {
	font-family: "Avenir", Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	background-color: #eeeeee;
	min-height: 100vh;
}
</style>
