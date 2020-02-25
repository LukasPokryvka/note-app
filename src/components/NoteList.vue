<template>
	<ul :class="[meshGrid ? 'note-list-mesh' : 'note-list-hamburger']">
		<Note
			v-for="(note, index) in notes"
			:key="index + 1"
			:note="note"
			:index="index"
			@delete-note="deleteNote"
			@edit-note="editNote"
			@confirm-note-edit="confirmNoteEdit"
		/>
	</ul>
</template>

<script>
import Note from "@/components/Note.vue";

export default {
	components: {
		Note
	},
	data() {
		return {
			meshGrid: true,
			notes: [
				{
					header: "Vitajte v aplikácii",
					text: "Aplikácia má slúžiť na vytváranie poznámok",
					timestamp: "5. 2. 2020, 0:53:38",
					edit: false
				},
				{
					header: "Obsah poznámok",
					text:
						"Poznámka sa skladá z názvu a tela, pod poznámkou sa nachádza čas a dátum, kedy bola poznámka vytvorená.",
					timestamp: "5. 2. 2020, 0:53:38",
					edit: false
				},
				{
					header: "Pridať/Vymazať",
					text:
						"Poznámku vytvoríte vyplnením nadpisu a tela poznámky, tieto polia sú povinné. Pridať ju je následne možné stlačením Enteru, alebo kliknutím na Pridať. Vymazať poznámku je možné pomocou krížika v pravom hornom rohu.",
					timestamp: "5. 2. 2020, 0:53:38",
					edit: false
				},
				{
					header: "Editácia",
					text:
						"Editovať poznámku je možné kliknutím na pero v pravom dolnom rohu. Po zmene textu sa uloží opätovným kliknutím na fajku.",
					timestamp: "5. 2. 2020, 0:53:38",
					edit: false
				},
				{
					header: "Uloženie",
					text:
						"Momentálne sa poznámky ukladajú do vnútornej pamäti, čiže na dow/up nie je potrebné internetovné pripojenie a sú dostupné aj po vypnutí zariadenia.",
					timestamp: "5. 2. 2020, 0:53:38",
					edit: false
				},
				{
					header: "Zmena vzhľadu",
					text:
						"Na vrchu aplikácie sa nachádza tlačidlo pre zmenu vzhľadu.",
					timestamp: "5. 2. 2020, 0:53:38",
					edit: false
				},
				{
					header: "Enclosure",
					text: "Prajem príjemné používanie 🎉 LP 👋",
					timestamp: "5. 2. 2020, 0:53:38",
					edit: false
				}
			]
		};
	},
	methods: {
		deleteNote(index) {
			this.notes.splice(index, 1);
		},
		editNote(noteToEdit) {
			this.notes.map(note => (note.edit = false));
			noteToEdit.edit = true;
		},
		confirmNoteEdit() {
			this.notes.map(note => (note.edit = false));
		}
	},
	mounted() {
		this.$root.$on("add-note", data => this.notes.push(data));
		this.$root.$on("change-grid", () => {
			this.meshGrid = !this.meshGrid;
			this.$root.$emit("grid-value-changed", this.meshGrid);
		});
		if (localStorage.notes) {
			this.notes = JSON.parse(localStorage.notes);
		}
	},
	watch: {
		notes(newNotes) {
			localStorage.notes = JSON.stringify(newNotes);
		}
	}
};
</script>

<style lang="scss">
.note-list-mesh,
.note-list-hamburger {
	font-family: "Caveat", cursive;
	width: 80%;
	margin: 0 auto;
	min-height: 100px;
	text-align: left;
	padding: 2em 0;

	li:nth-child(8n + 1) {
		background-color: #ffe26d;
	}
	li:nth-child(8n + 2) {
		background-color: #d4ff55;
	}
	li:nth-child(8n + 3) {
		background-color: #ccaa66;
	}
	li:nth-child(8n + 4) {
		background-color: #fea28b;
	}
	li:nth-child(8n + 5) {
		background-color: #c6ecff;
	}
	li:nth-child(8n + 6) {
		background-color: #60c85b;
	}
	li:nth-child(8n + 7) {
		background-color: #d894b4;
	}
	li:nth-child(8n + 8) {
		background-color: #328695;
	}

	.note {
		width: 100%;
		margin: 0 0 1em;
		word-break: break-word;
		padding: 0.7em;
		position: relative;
		transition: transform 0.3s ease-in;

		h2 {
			font-size: 1.7em;
			font-weight: bold;
		}
		p {
			font-size: 1.5em;
		}
		small {
			font-family: "Avenir", Helvetica, Arial, sans-serif;
			display: block;

			font-size: 0.5em;
			margin-top: 1em;
			color: #555;
		}
		a {
			display: none;
			width: 0.5em;
			position: absolute;
			right: 5px;
			cursor: pointer;

			img {
				max-width: 100%;
			}
		}

		textarea {
			background: none;
			border: none;
			overflow: hidden;
			outline: none;
		}
	}
	li.note:hover {
		transform: scale(1.03);

		a {
			display: inline-block;
		}
	}
}

.note-list-mesh {
	column-count: 4;
	column-gap: 1em;

	.note {
		display: inline-block;
		textarea {
			min-height: 150px;
		}
	}
}

.note-list-hamburger {
	.note {
		textarea {
			min-height: 80px;
			width: 100%;
		}
	}
}
</style>