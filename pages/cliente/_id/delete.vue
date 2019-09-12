<template>
  <div class="m-5">
    <b-col cols="12">
      <nuxt-link :to="{path: '/'}">
        <h1 class="text-center">Vue-Viva</h1>
      </nuxt-link>
    </b-col>
    <b-col>
      <h2 class="text-left">Deseja Exluir</h2>
      <h3>Deseja realmente deletar o cliente {{cliente.nome}}</h3>
      <b-button @click="excluirCliente" type="submit" class="float-center" variant="danger">Exluir</b-button>
      <b-button :to="{path: '/'}" type="submit" class="float-center" variant="primary">Cancelar</b-button>
    </b-col>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cliente: {
        id: null,
        nome: "",
      },
      status: [
        { text: "Nenhum Selecionado", value: null },
        "Ativo",
        "Excluido",
        "Inativo"
      ]
    }
  },
  mounted() {
    let idCliente = this.$route.params.id

    let clientes = this.$axios
      .get(`http://localhost:4300/clientes/${idCliente}`)
      .then(response => {
        this.cliente = response.data
      }, this)
  },
  methods: {
    excluirCliente(evt) {
      evt.preventDefault()
      let idCliente = this.$route.params.id

      let clientes = this.$axios
        .delete(`http://localhost:4300/clientes/${idCliente}`)
        .then(response => {
          this.$router.push("/")
        }, this)
    }
  }
}
</script>