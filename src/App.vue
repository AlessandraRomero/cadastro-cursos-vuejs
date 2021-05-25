<template>
  <div class="content">
    <CadastrarCursos />
    <br />
    <ListaCursos />
  </div>
</template>

<script>
import CadastrarCursos from "./components/CadastrarCursos";
import ListaCursos from "./components/ListaCursos";
export default {
  name: "App",
  components: {
    CadastrarCursos,
    ListaCursos,
  },
};
</script>

<style>
@import './css/cadastro.css';
@import './css/busca-lista.css';
</style>