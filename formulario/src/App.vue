<template>
  <div id="app">
    <h1>Registrar Reclamação</h1>
    <div class="conteudo">
      <form class="painel" v-if="!enviado">
        <div class="cabecalho">Formulário</div>
        <Rotulo nome="E-mail">
          <input type="text" v-model.lazy.trim="usuario.email" />
        </Rotulo>
        <Rotulo nome="Senha">
          <input type="password" v-model="usuario.senha" />
        </Rotulo>
        <Rotulo nome="Idade">
          <input type="number" v-model.number="usuario.idade" />
        </Rotulo>
        <Rotulo nome="Mensagem">
          <textarea name="" cols="20" rows="5" v-model="mensagem"></textarea>
        </Rotulo>
        <Rotulo nome="Características do Problema">
          <span class="mr-4"
            ><input
              type="checkbox"
              v-model="caracteristicas"
              value="reproduzivel"
            />
            Reproduzível</span
          >
          <span
            ><input
              type="checkbox"
              v-model="caracteristicas"
              value="intermitente"
            />
            Intermitente</span
          >
        </Rotulo>
        <Rotulo nome="Qual produto?">
          <span class="mr-4"
            ><input type="radio" value="Web" v-model="produto" /> Web</span
          >
          <span class="mr-4"
            ><input type="radio" value="Mobile" v-model="produto" />
            Mobile</span
          >
          <span
            ><input type="radio" value="Outro" v-model="produto" /> Outro</span
          >
        </Rotulo>
        <Rotulo nome="Prioridade">
          <select v-model="prioridade">
            <option
              v-for="prioridade in prioridades"
              :value="prioridade.codigo"
              :selected="prioridade.codigo === 1"
              :key="prioridade.codigo"
            >
              {{ prioridade.codigo }} - {{ prioridade.nome }}
            </option>
          </select>
        </Rotulo>
        <Rotulo nome="Primeira Reclamação?">
          <Escolha v-model="escolha" />
        </Rotulo>
        <hr />
        <button @click.prevent="enviar">Enviar</button>
      </form>
      <div class="painel" v-else>
        <div class="cabecalho">Resultados</div>
        <Rotulo nome="E-mail">
          <span>{{ usuario.email }}</span>
        </Rotulo>
        <Rotulo nome="Senha">
          <span>{{ usuario.senha }}</span>
        </Rotulo>
        <Rotulo nome="Idade">
          <span>{{ usuario.idade }}</span>
        </Rotulo>
        <Rotulo nome="Mensagem">
          <span style="white-space: pre">{{ mensagem }}</span>
          <!-- adicionei um estilo no span para preservar os espaços
          em branco no textarea. -->
        </Rotulo>
        <Rotulo nome="Características do Problema">
          <span>
            <ul>
              <li v-for="c in caracteristicas" :key="c">
                {{ c }}
              </li>
            </ul>
          </span>
        </Rotulo>
        <Rotulo nome="Qual Produto?">
          <span>{{ produto }}</span>
        </Rotulo>
        <Rotulo nome="Prioridade">
          <span>{{ prioridade }}</span>
        </Rotulo>
        <Rotulo nome="Primeira Reclamação?">
          <span>{{ escolha }}</span>
        </Rotulo>
      </div>
    </div>
  </div>
</template>

<script>
import Rotulo from "./components/Rotulo.vue";
import Escolha from "./components/Escolha.vue";

export default {
  name: "App",
  components: {
    Rotulo,
    Escolha,
  },
  methods: {
    enviar() {
      this.enviado = true;
    },
  },
  data() {
    return {
      caracteristicas: [],
      prioridade: 1,
      prioridades: [
        { codigo: 1, nome: "Baixa" },
        { codigo: 2, nome: "Moderada" },
        { codigo: 3, nome: "Alta" },
      ],
      mensagem: "",
      produto: "Web",
      usuario: {
        email: "",
        senha: "",
        idade: 21,
      },
      escolha: true,
      enviado: false,
    };
  },
};
</script>

<style>
body {
  background: #dae2f8;
  background: -webkit-linear-gradient(to right, #d6a4a4, #dae2f8);
  background: linear-gradient(to right, #d6a4a4, #dae2f8);
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  display: flex;
  flex-direction: column;
}
#app form button {
  float: left;
  margin: 10px 0px;
  padding: 10px 20px;
  font-size: 1.4rem;
  border-radius: 5px;
  background-color: #d6a4a4;
}

.conteudo {
  display: flex;
}
.painel {
  flex: 1;
  background: #fff;
  margin: 0px 10px;
  padding: 20px;
  border: 1px solid #aaa;
  border-radius: 5px;
}

.painel .cabecalho {
  width: 100%;
  background-color: #ddd;
  padding: 10px 0px;
  border-radius: 5px;
  font-size: 1.4rem;
}

#app h1 {
  font-weight: 300;
  margin: 20px;
  padding: 0;
}

.mr-4 {
  margin-right: 40px;
}
</style>
