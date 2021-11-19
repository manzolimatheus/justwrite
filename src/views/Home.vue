<template>
  <div class="home">
    <div class="grid">
      <div class="text">
        <h1>Seu bloco de notas, totalmente anônimo e seguro.</h1>
        <br>
        <p>JustWrite é um bloco de notas online, onde você pode organizar seus pensamentos,
          tarefas, deveres, ou até mesmo anotações básicas. Seus textos ficam salvos diretamente
          em seu navegador, não se preocupe com ninguém olhando!
        </p>
        <br>
        <router-link to="notes">Começar a escrever</router-link>
      </div>
      <div class="image">
        <img src="https://image.flaticon.com/icons/png/512/138/138938.png" alt="Escrita em Banco de dados">
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "Home",
  components: {
  },
};
</script>

<style>
.grid{
  display: grid;
  grid-template-columns: repeat(2, 1fr) ;
  text-align: center;
}

.text{
  padding: 10% 10% 10% 10%;
}

.text a{
  background-color: #43e087;
  text-decoration: none;
  padding: 2%;
  color: black;
  border-radius: 10px;
}

.image img{
  width: 50%;
  padding: 10% 0 10% 0;
}

@media (max-width: 768px) {
  .grid{
    grid-template-columns: 100% ;
  }
}

</style>
