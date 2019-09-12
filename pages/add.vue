<template>
  <div class="m-5">
    <b-col cols="12">
      <nuxt-link :to="{path: '/'}">
        <h1 class="text-center">Vue-Viva</h1>
      </nuxt-link>
    </b-col>
    <b-form @submit="onSubmit">
      <h2 class="text-left">Cadatrar Cliente</h2>

      <cliente-form :cliente="cliente" :status="status"></cliente-form>

      <b-button type="submit" class="float-right" variant="primary">Salvar</b-button>
    </b-form>
  </div>
</template>

<script>
import ClienteForm from "../components/cliente-form.vue"

export default {
  components: { ClienteForm },
  data() {
    return {
      cliente: {
        id: null,
        nome: "",
        endereco: "",
        telefone: "",
        status: null,
        dtNascimento: ""
      },
      status: [
        { text: "Nenhum Selecionado", value: null },
        "Ativo",
        "Excluido",
        "Inativo"
      ]
    }
  },
  methods: {
    async onSubmit(evt) {
      evt.preventDefault()

      await this.$axios
        .post("http://localhost:4300/clientes", this.cliente)
        .then(response => response.data)
      this.$router.push("/")
    }
  }
}
</script>