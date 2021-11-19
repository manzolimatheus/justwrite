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
        <div class="col-10">
          <span class="badge bg-secondary">{{ note.id }}</span> -
          {{ note.title }}
        </div>
        <div class="col-2">
          <button
            class="btn btn-danger"
            @click="DeleteItem(notes.indexOf(note))"
          >
            <ion-icon name="trash-outline"></ion-icon>
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
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