<template>
	<li class="note">
		<h2>{{ note.header }}</h2>
		<a @click="deleteNote(index)" class="delete-note"
			><img src="@/assets/deleteNote.svg" alt="delete note"
		/></a>
		<p v-if="!note.edit">
			{{ note.text }}
			<small>Vytvorené: {{ note.timestamp }}</small>
			<a @click="noteEdit(note)" class="edit-note"
				><img src="@/assets/editNote.svg" alt="edit note"
			/></a>
		</p>
		<textarea v-if="note.edit" v-model="note.text"> </textarea>
		<a v-if="note.edit" class="confirm-edit-note" @click="confirmNoteEdit"
			><img src="@/assets/confirmEditNote.svg" alt="confirm edit note"
		/></a>
	</li>
</template>

<script>
export default {
	props: ["note", "index"],
	methods: {
		deleteNote(index) {
			this.$emit("delete-note", index);
		},
		noteEdit(note) {
			this.$emit("edit-note", note);
		},
		confirmNoteEdit() {
			this.$emit("confirm-note-edit");
		}
	}
};
</script>

<style lang="scss" >
.delete-note {
	top: 1px;
}
.edit-note {
	bottom: 8px;
}
.confirm-edit-note {
	bottom: 3px;
	width: 0.7em;
}
</style>