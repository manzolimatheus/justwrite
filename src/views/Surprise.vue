<template>
  <div id="about">
    <div class="row w-100 g-0">
      <div class="col-sm">
        <div class="container mt-5 p-3">
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
          <p>- De toda a sala, 19 de Novembro de 2021</p>

          <lottie-player
            src="https://assets10.lottiefiles.com/private_files/lf30_mmejwv1s.json"
            background="transparent"
            speed="1"
            style="width: 150px"
            loop
            autoplay
          ></lottie-player>
        </div>
      </div>
      <div class="col-sm">
        <div class="img"></div>
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
.img {
  background-image: url("/img/img01.jpeg");
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  width: 100%;
  height: 100vh;
}
</style>
