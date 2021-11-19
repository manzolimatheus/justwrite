<template>
  <div id="noteshow" class="m-3">
    <div v-if="note_selected != null">
      <span class="badge bg-secondary">{{ note_selected.id }}</span> <input type="text" v-model="title" @change="Save()" class="input-zero">
      <br><br>
      <textarea v-model="text" @change="Save" class="w-100 form-control"></textarea>
      <p class="alert alert-success mt-3" v-show="msg">Texto salvo com sucesso.</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "NoteShow",
  props: ["note"],
  data() {
    return {
      note_selected: null,
      title: null,
      text: null,
      msg: false,
    };
  },
  methods: {
    ShowNote() {
      let notes = JSON.parse(localStorage.getItem("notes"));
      this.note_selected = notes[this.note];
      this.text = this.note_selected.data;
      this.title = this.note_selected.title;
    },
    Save() {
      this.note_selected.data = this.text;
      this.note_selected.title = this.title;
      let notes = JSON.parse(localStorage.getItem("notes"));
      notes[this.note].data = this.text;
      notes[this.note].title = this.title;
      localStorage.setItem("notes", JSON.stringify(notes));
      this.msg = true;
      setTimeout(() => (this.msg = false), 1500);
      this.$emit('edit')
    },
  },
  watch: {
    note: function () {
      if (this.note != null){
        this.ShowNote();
      }else{
        this.note_selected = null
      }
    },
  },
};
</script>

<style scoped>
textarea {
  width: 100%;
}

.input-zero{
  border: 0;
  background: none;
}
</style>