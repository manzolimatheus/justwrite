<template>
  <div id="notesbuttons" class="m-3">
    <div class="row">
      <div class="col-sm">
        <button
          class="btn btn-info mt-3 w-100"
          data-bs-toggle="modal"
          data-bs-target="#MyModal"
        >
          <ion-icon name="add-circle-outline"></ion-icon> Nova nota
        </button>
      </div>
      <div class="col-sm">
        <button class="btn btn-danger mt-3 w-100" @click="clearNotes">
          <ion-icon name="close-circle-outline"></ion-icon> Excluir notas
        </button>
      </div>
    </div>

    <Modal @post="newNote" />
  </div>
</template>

<script>
import Modal from "@/components/Modal.vue";

export default {
  name: "NotesButtons",
  components: {
    Modal,
  },
  data() {
    return {
      notes: [],
    };
  },
  methods: {
    newNote(obj) {
      if (JSON.parse(localStorage.getItem("notes")) !== null) {
        this.notes = JSON.parse(localStorage.getItem("notes"));
      }
      this.notes.push({
        id: obj.id,
        title: obj.title,
        data: obj.data,
      });
      localStorage.setItem("notes", JSON.stringify(this.notes));
      this.$emit("refresh");
    },
    clearNotes() {
      this.notes = [];
      localStorage.removeItem("notes");
      this.$emit("list-clear");
    },
  },
  mounted() {
    if (JSON.parse(localStorage.getItem("notes")) !== null) {
      this.notes = JSON.parse(localStorage.getItem("notes"));
    }
  },
};
</script>

<style>
</style>