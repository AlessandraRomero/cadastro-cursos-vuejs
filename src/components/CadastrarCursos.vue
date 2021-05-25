<template>
  <div class="content">
    <img src="../assets/logo.png" alt="logo" />
    <h1>Cadastro de Cursos</h1>
    <section class="cadastro">
      <form class="form">
        <label for="nome">
          <span class="nome">Nome:</span>
          <input
            type="text"
            id="nome"
            name="nome"
            placeholder="nome"
            @change="$v.curso.nome.$touch()"
            v-model="curso.nome"
          />
          <p v-if="$v.curso.nome.$error">
            O campo "nome" precisa ser preenchido
          </p>
        </label>

        <label for="dataInicio">
          <span class="dataInicio"> Data de início:</span>
          <input
            type="date"
            id="dataInicio"
            name="dataInicio"
            v-model="curso.dataInicio"
            required
          />
          <p v-if="$v.curso.dataInicio.$error">
            O campo "data de inicio" precisa ser preenchido
          </p>
        </label>

        <label for="dataFim">
          <span class="dataFim"> Data de fim:</span>
          <input
            type="date"
            id="dataFim"
            name="dataFim"
            v-model="curso.dataFim"
            required
          />
          <p v-if="$v.curso.dataFim.$error">
            O campo "data de fim" precisa ser preenchido
          </p>
        </label>

        <label for="duracao">
          <span class="duracao">Duração (semanas):</span>
          <input
            type="number"
            id="duracao"
            name="duracao"
            placeholder="Duração em semanas"
            v-model="curso.duracao"
            required
          />
          <p v-if="$v.curso.duracao.$error">
            O campo "Duração" precisa ser preenchido
          </p>
        </label>

        <label for="descricao">
          <span class="descricao">Descrição:</span>
          <input
            type="text"
            id="descricao"
            name="descricao"
            placeholder="Descrição do curso"
            v-model="curso.descricao"
            required
          />
          <p v-if="$v.curso.descricao.$error">
            O campo "Descrição" precisa ser preenchido
          </p>
        </label>
        <div class="btnContent">
          <button
            type="button"
            class="btnCadastrar"
            v-on:click="cadastrarCurso(curso)"
          >
            Cadastrar
          </button>
        </div>
      </form>
    </section>
  </div>
</template>

<script>
import { required } from "vuelidate/lib/validators";
export default {
  name: "CadastrarCursos",
  data() {
    return {
      cursos: [],
      curso: {
        id: "",
        nome: "",
        dataInicio: "",
        dataFim: "",
        duracao: "",
        descricao: "",
      },
    };
  },
  validations: {
    curso: {
      nome: { required },
      dataInicio: { required },
      dataFim: { required },
      duracao: { required },
      descricao: { required },
    },
  },
  methods: {
    //Método para cadastrar um curso
    cadastrarCurso: function (curso) {
      let cursos = localStorage.getItem("cursosApp");

      //(Servirá como um id)adiciona um id rápido para cada curso
      curso.id = new Date().getTime();

      if (!this.$v.$invalid) {
        if (cursos) {
          cursos = JSON.parse(cursos);
          cursos.push(curso);
        } else {
          cursos = [curso];
        }
        
        window.location.reload();

        //atualiza localStorage
        localStorage.setItem("cursosApp", JSON.stringify(cursos));
      } else {
        this.$v.$touch();
      }
    },
  },
};
</script>


