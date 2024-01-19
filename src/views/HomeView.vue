<script setup>
import Table from '@/components/Table.vue';
import ModalCadastro from '@/components/ModalCadastro.vue';
</script>

<template>
  <header class="pt-5 d-flex justify-content-center align-items-center w-100">
    <h1>NUNES SPORT </h1>
  </header>
  <main class="d-flex justify-content-center">
    <section class="pt-2 container-fluid">
      <ModalCadastro class="mb-3" />
      <Table />
    </section>
  </main>
</template>

<style scoped>
main {
  height: fit-content;
}

h1 {
  font-family: 'Courier New', Courier, monospace;
  background-image: linear-gradient(to bottom, rgb(255, 230, 0), rgb(208, 255, 0), rgb(7, 255, 61));
  color: black;
  background-clip: text;
  -webkit-background-clip: text;

  /* Adicionado: */
  -webkit-text-fill-color: transparent;
  font-size: 4vw;
}

section {
  width: 85vw;
}

@media screen and  (max-width: 440px){
  h1 {
    font-size: 7vw;
    margin-bottom: 2vh;
  }
}
</style>
