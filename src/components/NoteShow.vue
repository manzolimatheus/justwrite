<template>
  <div id="noteshow" class="m-3">
    <div v-if="note_selected != null">
      <span class="badge bg-secondary">{{ note_selected.id }}</span>
      <input type="text" v-model="title" @change="Save()" class="input-zero ms-1 w-75" maxlength="40" />
      <br>
      <span v-show="msg" class="text-success ms-1">Nota salva com sucesso.</span>
      <br /><br />
      <textarea
        v-model="text"
        @change="Save"
        class="w-100 form-control"
      ></textarea>
      <br>
      <img :src="img_url" alt="Imagem anexada" class="img shadow" id="img" v-if="img_url != ''" />
      <br>
       <input
        type="url"
        id="img_url"
        v-model="img_url"
        class="input-zero w-100"
        @change="Save"
        placeholder="Insira um link de imagem para exibir uma imagem em sua nota."
      />
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
      img_url: null,
    };
  },
  methods: {
    ShowNote() {
      let notes = JSON.parse(localStorage.getItem("notes"));
      this.note_selected = notes[this.note];
      this.text = this.note_selected.data;
      this.title = this.note_selected.title;
      this.img_url = this.note_selected.img;
    },
    Save() {
      this.note_selected.data = this.text;
      this.note_selected.title = this.title;
      this.note_selected.img = this.img_url;
      let notes = JSON.parse(localStorage.getItem("notes"));
      notes[this.note].data = this.text;
      notes[this.note].title = this.title;
      notes[this.note].img = this.img_url;
      localStorage.setItem("notes", JSON.stringify(notes));
      this.msg = true;
      setTimeout(() => (this.msg = false), 1500);
      this.$emit("edit");
    },
  },
  watch: {
    note: function () {
      if (this.note != null) {
        this.ShowNote();
      } else {
        this.note_selected = null;
      }
    },
  },
};
</script>

<style scoped>
textarea {
  width: 100%;
}

.input-zero {
  border: 0;
  background: none;
}

.img{
  width: 100%;
  border-radius: 10px;
  object-fit: cover;
}
</style>