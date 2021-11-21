<template>
  <div id="notes">
    <NotesButtons @refresh="RefreshComponent" @list-clear="UpdateAll" />
    <div class="row w-100">
      <div class="col-sm">
        <NotesList
          :trigger="update"
          @note-selected="ShowNote"
          @empty-list="HideNote"
          @disable-show="HideNote"
        />
      </div>
      <div class="col-sm">
        <NoteShow :note="selected_note" @edit="RefreshComponent" />
      </div>
    </div>
  </div>
</template>

<script>
import NotesList from "@/components/NotesList.vue";
import NotesButtons from "@/components/NotesButtons.vue";
import NoteShow from "@/components/NoteShow.vue";

export default {
  name: "Notes",
  components: {
    NotesList,
    NotesButtons,
    NoteShow,
  },
  data() {
    return {
      update: false,
      selected_note: null,
    };
  },
  methods: {
    RefreshComponent() {
      this.update = !this.update;
    },
    ShowNote(id) {
      this.selected_note = id;
    },
    HideNote() {
      this.selected_note = null;
    },
    UpdateAll() {
      this.RefreshComponent();
      this.HideNote();
    },
  },
};
</script>

<style></style>
