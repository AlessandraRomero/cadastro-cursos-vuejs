<template>
  <div class="content">
    <section class="pesquisaCursos">
      <input
        type="search"
        class="form-control"
        id="pesquisaNome"
        placeholder="Pesquisar curso"
        v-model="nome"
      />
      <button
        class="btn btn-primary btn-buscar"
        v-on:click="pesquisarCurso(nome)"
      >
        Buscar
      </button>
    </section>
    <div class="tabelaCursos">
      <table class="table table-striped table-hover">
        <thead>
          <tr>
            <th scope="col">Nome</th>
            <th scope="col">Data de início</th>
            <th scope="col">Data de Término</th>
            <th scope="col">Duração</th>
            <th scope="col">Descrição</th>
            <th></th>
          </tr>
        </thead>
        <tbody id="listaCursos">
          <tr v-for="curso in filtered" :key="curso.nome">
            <td>{{ curso.nome }}</td>
            <td>{{ curso.dataInicio }}</td>
            <td>{{ curso.dataFim }}</td>
            <td>{{ curso.duracao }}</td>
            <td>{{ curso.descricao }}</td>
            <td>
              <button class="btn-excluir" v-on:click="excluirCurso(curso.id)">
                Remover
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "ListaCursos",
  data() {
    return {
      cursos: [],
      filtered: [],
      nome: ''

    };
  },
  created() {
    this.cursos = JSON.parse(localStorage.getItem("cursosApp"));
    this.filtered = JSON.parse(localStorage.getItem("cursosApp"));
  },
  methods: {
    //função para excluir um registro
    excluirCurso: function (cursoId) {
      let cursos = localStorage.getItem("cursosApp");

      if (!cursos) return;

      cursos = JSON.parse(cursos);

      cursos = cursos.filter((curso) => {
        return curso.id != cursoId;
      });

      window.location.reload()
      localStorage.setItem("cursosApp", JSON.stringify(cursos));
    },
    //funcão para filtrar um curso por nome
    pesquisarCurso: function () {
      this.filtered = this.cursos;

      //se o campo estiver vazio não vai pesquisar nada
      if (this.nome === "" || this.nome === " ") {
        this.filtered = this.cursos;

      } else {
        this.filtered = this.cursos.filter((cursoNome) => {
          return cursoNome.nome.includes(this.nome);
        });
      }
    },
  },
};
</script>


