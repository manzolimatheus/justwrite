<template>
  <div id="noteslist" class="m-3">
    <h3>Notas ({{ notes.length }})</h3>
    <p v-if="notes.length < 1">Nenhuma nota para exibir.</p>
    <div
      class="w-100 shadow bg-white mb-3 p-1 rounded item-container"
      v-for="note in notes"
      :key="note.id"
      @click="ShowNote(notes.indexOf(note))"
    >
      <div class="row">
        <div class="col-9">
          <span class="badge bg-secondary">{{ note.id }}</span> -
          {{ note.title }}
        </div>
        <div class="col-3">
          <div class="row w-100">
            <div class="col">
              <button
                class="btn btn-danger"
                @click="DeleteItem(notes.indexOf(note))"
              >
                <ion-icon name="trash-outline"></ion-icon>
              </button>
            </div>
            <div class="col">
              <button
                class="btn btn-info"
                @click="DownloadItem(notes.indexOf(note))"
              >
                <ion-icon name="download-outline"></ion-icon>
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { saveAs } from "file-saver";

export default {
  name: "NotesList",
  props: {
    trigger: Boolean,
  },
  data() {
    return {
      notes: [],
    };
  },
  methods: {
    Refresh() {
      if (JSON.parse(localStorage.getItem("notes")) !== null) {
        this.notes = JSON.parse(localStorage.getItem("notes"));
      } else {
        this.notes = [];
      }
    },
    ShowNote(id) {
      this.$emit("note-selected", id);
    },
    DeleteItem(id) {
      console.log(id);
      this.notes.splice(id, 1);
      localStorage.setItem("notes", JSON.stringify(this.notes));
      this.Refresh();
      this.$emit("disable-show");

      if (this.notes.length < 1) {
        this.$emit("empty-list");
      }
    },
    DownloadItem(id) {
      const note = this.notes[id];
      const today = new Date();
      const file = `
      <html>
      <head>
      <title>${note.title}</title>
      <style>

        *{
          font-family: Arial, Helvetica, sans-serif;
        }

        em{
          color: grey;
        }

        textarea{
          border: 0;
          font-size: 12pt;
          background-color: transparent;
          resize: none;
          outline: none;
        }

        img{
          border-radius: 10px;
        }

        .container{
          display: grid;
          grid-template-columns: repeat(3, 1fr);
        }
      </style>
      </head>
      <body>
      <div class="container">
      <div></div>
      <div>
      <h1>${note.title}</h1>
      <em>Registrado em ${today.getDate()}/${today.getMonth()}/${today.getFullYear()}</em>
      <br><br>
      ${note.img != "" ? `<img src="${note.img}" width="100%">` : ""}
      <br><br>
      <textarea rows="60" cols="60">${note.data}</textarea>
      </div>
      <div></div>
      </div>
      </body>
      </html>
      `;
      var blob = new Blob([file], { type: "text/html;charset=utf-8" });

      saveAs(blob, `${note.title}.html`);
    },
  },
  watch: {
    trigger: function () {
      this.Refresh();
    },
  },
  mounted() {
    if (JSON.parse(localStorage.getItem("notes")) !== null) {
      this.notes = JSON.parse(localStorage.getItem("notes"));
    }
  },
};
</script>

<style scoped>
.item-container {
  cursor: pointer;
}

.item-container:hover {
  transform: scale(1.05);
}
</style>
