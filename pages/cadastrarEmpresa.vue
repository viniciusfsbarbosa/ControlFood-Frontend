<template>
  <main class="background">
    <nav class="navbar navbar-expand navbar-dark" style="background-color: #009879;">
      <NuxtLink to="/dashboardSite" class="navbar-brand">Control Food</NuxtLink>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarsExample02"
        aria-controls="navbarsExample02"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarsExample02">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <NuxtLink to="/cadastrarEmpresa" class="nav-link"
              >Cadastrar Empresas</NuxtLink
            >
          </li>
          <li class="nav-item active">
            <NuxtLink to="/cadastrarColaborador" class="nav-link"
              >Cadastrar Colaborador</NuxtLink
            >
          </li>
          <li class="nav-item active">
            <NuxtLink to="/listarColaboradores" class="nav-link"
              >Listar Colaboradores</NuxtLink
            >
          </li>
          <li class="nav-item active">
            <NuxtLink to="/listarEmpresas" class="nav-link"
              >Listar Empresas</NuxtLink
            >
          </li>
          <li class="nav-item active">
            <NuxtLink to="/relatorioGeral" class="nav-link"
              >Relatórios</NuxtLink
            >
          </li>
          <li>
            <button class="botaosair" @click="logout()">Sair</button>
          </li>
        </ul>
      </div>
    </nav>
    <div class="container">
      <div class="row">
        <div class="col-6">
          <div class="card ajustes">
            <div class="card-body">
              <h1>Cadastrar Empresa</h1>
              <form @submit.prevent="cadastro">
                <b-alert :variant="responseColor" :show="showAlert">{{
                  responseMessage
                }}</b-alert>

                <div>
                  <label for="nome">CNPJ:</label>
                  <input
                    v-model="empresa.cnpj"
                    class="form-control"
                    type="text"
                    name="nome"
                    id="cnpj"
                    placeholder="CNPJ"
                    v-maska="'##.###.###/####-##'"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">Nome da empresa:</label>
                  <input
                    v-model="empresa.nomeEmpresa"
                    class="form-control"
                    type="text"
                    placeholder="Nome da Empresa"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">E-mail:</label>
                  <input
                    v-model="empresa.email"
                    class="form-control"
                    type="email"
                    placeholder="E-mail"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">Nome do Responsável:</label>
                  <input
                    v-model="empresa.nomeResponsavel"
                    class="form-control"
                    type="text"
                    placeholder="Nome da Empresa"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="email">Contato do Responsável:</label>
                  <input
                    v-model="empresa.contatoResponsavel"
                    class="form-control"
                    type="text"
                    placeholder="Contato do Responsável"
                    required
                  />
                </div>
                <div class="form-group">
                  <label for="inputAddress">Endereço</label>
                  <input
                    v-model="empresa.endereco"
                    type="text"
                    class="form-control"
                    placeholder="Rua Major Gote, n° 808"
                    required
                  />
                </div>
                <div class="form-row">
                  <div class="form-group col-md-6">
                    <label for="inputCity">Cidade</label>
                    <input
                      v-model="empresa.cidade"
                      type="text"
                      class="form-control"
                      placeholder="Patos de Minas"
                      required
                    />
                  </div>
                  <div class="form-group col-md-3">
                    <label for="inputEstado">Estado</label>
                    <input
                      v-model="empresa.estado"
                      type="text"
                      class="form-control"
                      id="estado"
                      placeholder="MG"
                      v-maska="'AA'"
                      required
                    />
                  </div>
                </div>

                <div class="form-group text-center">
                  <button type="submit" class="btn btn-dark">Cadastrar</button>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import { maska } from 'maska'

export default {
  directives: { maska },
  data: () => ({
    empresa: {
      cnpj: '',
      nomeEmpresa: '',
      email: '',
      nomeResponsavel: '',
      contatoResponsavel: '',
      endereco: '',
      cidade: '',
      estado: '',
      cep: '',
      user_id: parseInt(localStorage.getItem('id')),
    },
    responseColor: null,
    responseMessage: null,
    showAlert: false,
  }),

  methods: {
    async cadastro() {
      /**
       * Post = Enviar dados
       * Get = Receber dados
       * Patch = Atualizar dados
       * Delete = Excluir dados
       */
      try {
        const response = await this.$axios.$post('/empresa', this.empresa)
        this.responseColor = 'success'
        this.responseMessage = response.message
        this.showAlert = true
      } catch (error) {
        this.responseColor = 'danger'
        this.responseMessage = 'Ocorreu um erro'
        this.showAlert = true
      }
    },
     logout() {
      localStorage.removeItem('token')
      localStorage.removeItem('id')
      this.$router.push({ name: 'index' })
    },
  },
}
</script>

<style>

* {
  font-family: sans-serif; 
}

.row {
  margin-top: 3%;
  justify-content: center;
}
.ajustes {
  margin-bottom: 12%;
}
.botaosair{
  background-color: #009879;
  color: #fff;
  border:none;
  padding:27%;
}

</style>
