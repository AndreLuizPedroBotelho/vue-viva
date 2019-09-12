<template>
  <div class="m-5">
    <b-col cols="12">
      <h1 class="text-center">Vue-Viva</h1>
    </b-col>
    <nuxt-link class="btn btn-default" :to="{path: '/add'}">
      <span class="glyphicon glyphicon-plus"></span>
      Adicionar Cliente
    </nuxt-link>
    <b-button type="button" @click="csvExport(csvData)" variant="primary">Exportar</b-button>


    <b-col cols="12">
      <mdb-datatable :data="data" striped bordered />
    </b-col>
  </div>
</template>

<script>
import { LayoutPlugin } from "bootstrap-vue"
import { mdbDatatable } from "mdbvue"

export default {
  components: {
    LayoutPlugin,
    mdbDatatable,
  },
  data() {
    return {
      data: {
        columns: [
          {
            label: "Código",
            field: "id",
            sort: "asc"
          },
          {
            label: "Nome",
            field: "nome",
            sort: "asc"
          },
          {
            label: "Endereço",
            field: "endereco",
            sort: "asc"
          },
          {
            label: "Telefone",
            field: "telefone",
            sort: "asc"
          },
          {
            label: "Status",
            field: "status",
            sort: "asc"
          },
          {
            label: "Data de nascimento",
            field: "dtNascimento",
            sort: "asc"
          },
          {
            label: "Ações",
            field: "action"
          }
        ],
        rows: []
      },    
      clientes: [],
    }
  },
  computed: {
    csvData() {
      return this.clientes.map(item => ({
        ...item,

      }));
    }
  },
  mounted() {
    let clientes = this.$axios
      .get("http://localhost:4300/clientes")
      .then(response => {
        response.data.forEach(function(obj) {
          const cliente = Object.assign({}, obj);
          cliente.dtNascimento = new Date(cliente.dtNascimento)
          cliente.dtNascimento = cliente.dtNascimento.toLocaleDateString()
          this.clientes.push(cliente)

          obj.dtNascimento = new Date(obj.dtNascimento)
          obj.dtNascimento = obj.dtNascimento.toLocaleDateString()

          obj.action = `<a href="/cliente/${obj.id}/edit" class="btn btn-primary btn-sm"><span class="glyphicon glyphicon-plus"></span>
            Editar 
             </a> &nbsp;
            <a href="/cliente/${obj.id}/delete" class="btn btn-danger btn-sm"><span class="glyphicon glyphicon-plus"></span>
            Deletar
            </a>`
          this.data.rows.push(obj)
        }, this)
      }, this)
  },
    methods: {
    csvExport(arrData) {
      let csvContent = "data:text/csv;charset=utf-8,";
      csvContent += [
        Object.keys(arrData[0]).join(";"),
        ...arrData.map(item => Object.values(item).join(";"))
      ]
        .join("\n")
        .replace(/(^\[)|(\]$)/gm, "");

      const data = encodeURI(csvContent);
      const link = document.createElement("a");
      link.setAttribute("href", data);
      link.setAttribute("download", "export.csv");
      link.click();
    }
  },
  openEdit() {
    this.$router.push("/edit")
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
}
</style>
