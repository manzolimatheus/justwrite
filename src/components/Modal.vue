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
              <label for="title">Título *</label>
              <input
                type="text"
                v-model="title"
                id="title"
                class="form-control"
                @input="checkEmpty"
              />
              <br />
              <label for="data">Texto *</label>
              <textarea
                id="data"
                v-model="data"
                class="form-control"
                @input="checkEmpty"
              ></textarea>
              <br />
              <div class="row">
                <div class="col-sm">
                  <label for="img_url">Anexar imagem - Link (Opcional)</label>
                  <input
                    type="url"
                    id="img_url"
                    v-model="img_url"
                    class="form-control"
                    @input="LoadImage"
                  />
                </div>
                <div class="col-sm">
                  <img
                    :src="img_url"
                    alt="Imagem anexada"
                    class="img shadow"
                    id="img"
                  />
                </div>
              </div>
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
          <button
            type="button"
            id="submitButton"
            class="btn btn-primary"
            @click="newNote"
            disabled
          >
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
      data: "",
      title: "",
      img_url: "",
    };
  },
  methods: {
    newNote() {
      if (this.data.includes("@surprise") === true) {
        document.querySelector("body > div.modal-backdrop.fade.show").remove();
        this.$router.push("/surprise");
      } else {
        if (JSON.parse(localStorage.getItem("notes")) !== null) {
          let notes = JSON.parse(localStorage.getItem("notes"));
          this.$emit("post", {
            id: notes.length + 1,
            data: this.data,
            title: this.title,
            img: this.img_url,
          });
        } else {
          this.$emit("post", {
            id: 1,
            data: this.data,
            title: this.title,
            img: this.img_url,
          });
        }
        this.title = "";
        this.data = "";
        this.img_url = "";
        document.querySelector("#submitButton").disabled = true;
        document.querySelector("#img").style.display = "none";
      }
    },
    checkEmpty() {
      const button = document.querySelector("#submitButton");

      if (this.data != "" && this.title != "") {
        button.disabled = false;
      } else {
        button.disabled = true;
      }
    },
    LoadImage() {
      document.querySelector("#img").style.display = "block";
    },
  },
  mounted() {
    document.querySelector("#img").style.display = "none";
  },
};
</script>

<style scoped>
.img {
  width: 100%;
  height: 100px;
  border-radius: 10px;
  object-fit: cover;
}
</style>