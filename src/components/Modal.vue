<template>
  <div
    class="modal fade"
    id="MyModal"
    tabindex="-1"
    aria-labelledby="exampleModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">
            Escrevendo: {{ title }}
          </h5>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <div class="form">
            <form @onsubmit.prevent="newNote">
              <label for="title">Título</label>
              <input
                type="text"
                v-model="title"
                id="title"
                class="form-control"
                required
              />
              <br />
              <label for="data">Texto</label>
              <textarea
                id="data"
                v-model="data"
                class="form-control"
                required
              ></textarea>
              <br />
            </form>
          </div>
        </div>
        <div class="modal-footer">
          <button
            type="button"
            class="btn btn-secondary"
            data-bs-dismiss="modal"
          >
            Cancelar
          </button>
          <button type="button" class="btn btn-primary" @click="newNote">
            Salvar
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Modal",
  data() {
    return {
      data: null,
      title: null,
    };
  },
  methods: {
    newNote() {
      if (this.data.includes('@surprise') == true){
        document.querySelector("body > div.modal-backdrop.fade.show").remove()
        this.$router.push('/surprise')
      }else{
      if (JSON.parse(localStorage.getItem("notes")) !== null) {
        const today = new Date();
        let notes = JSON.parse(localStorage.getItem("notes"));
          console.log()
        this.$emit("post", {
          id: notes.length + 1,
          data: this.data
            .replace(
              "@date",
              `${today.getDate()}/${today.getMonth()}/${today.getFullYear()} - ${today.getHours()}:${today.getMinutes()}`
            ),
          title: this.title,
        });
      } else {
        this.$emit("post", { id: 1, data: this.data, title: this.title });
      }
      this.title = "";
      this.data = "";
      }
    },
  },
};
</script>

<style>
</style>