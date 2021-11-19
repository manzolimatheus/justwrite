<template>
  <div id="about">
    <div class="row w-100">
      <div class="col-sm">
        <div class="container mt-5">
          <h1>Querido professor,</h1>
          <p>
            Querido professor Nilton, adoramos passar esses três anos com você e
            com todos os outros professores, tivemos ótimos momentos juntos,
            você nos ensinou muito e deu base para nossa profissão e paixão.
            Muito obrigado por tudo, pela calma, paciência ao explicar, ajuda em
            nosso desenvolvimento. Agora, professor, em nome de toda a sala,
            aceita ser nosso Paraninfo e nos acompanhar ao fim dessa jornada? ♥
            A propósito, espero que goste de pinguins!
          </p>
          <p>- De toda a sala - 19 de Novembro de 2021</p>

          <lottie-player
            src="https://assets10.lottiefiles.com/private_files/lf30_mmejwv1s.json"
            background="transparent"
            speed="1"
            style="width: 150px;"
            loop
            autoplay
          ></lottie-player>
        </div>
      </div>
      <div class="col-sm">
        <div class="container">
          <div
            id="carouselExampleControls"
            class="carousel slide"
            data-bs-ride="carousel"
          >
            <div class="carousel-inner">
              <div class="carousel-item active">
                <img src="/img/img01.jpeg" class="d-block w-100" alt="..." />
              </div>
              <div class="carousel-item">
                <img src="/img/img02.jpeg" class="d-block w-100" alt="..." />
              </div>
              <div class="carousel-item">
                <img src="/img/img03.jpeg" class="d-block w-100" alt="..." />
              </div>
            </div>
            <button
              class="carousel-control-prev"
              type="button"
              data-bs-target="#carouselExampleControls"
              data-bs-slide="prev"
            >
              <span
                class="carousel-control-prev-icon"
                aria-hidden="true"
              ></span>
              <span class="visually-hidden">Previous</span>
            </button>
            <button
              class="carousel-control-next"
              type="button"
              data-bs-target="#carouselExampleControls"
              data-bs-slide="next"
            >
              <span
                class="carousel-control-next-icon"
                aria-hidden="true"
              ></span>
              <span class="visually-hidden">Next</span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Surprise",
};
</script>

<style scoped>
</style>