<template>
  <div class="m-5 col-11">
    <b-form-group id="input-group-1" label="Nome:" label-for="input-1">
      <b-form-input id="input-1" v-model="cliente.nome" type="text" placeholder="Digite o nome"></b-form-input>
    </b-form-group>

    <b-form-group id="input-group-2" label="Endereço:" label-for="input-2">
      <b-form-input
        id="input-2"
        v-model="cliente.endereco"
        type="text"
        placeholder="Digite o endereço"
      ></b-form-input>
    </b-form-group>

    <b-form-group id="input-group-3" label="Telefone:" label-for="input-3">
      <b-form-input
        id="input-3"
        v-model="cliente.telefone"
        type="tel"
        placeholder="Digite o telefone"
      ></b-form-input>
    </b-form-group>

    <b-form-group id="input-group-4" label="Status:" label-for="input-4">
      <b-form-select id="input-4" v-model="cliente.status" :options="status"></b-form-select>
    </b-form-group>

    <b-form-group id="input-group-5" label="Data de nascimento:" label-for="input-5">
      <b-form-input
        id="input-5"
        v-model="cliente.dtNascimento"
        type="date"
        placeholder="Digite a data de nascimento"
      ></b-form-input>
    </b-form-group>
  </div>
</template>


<script>
export default {
  name: "ClienteForm",
  props: ["cliente", "status"]
}
</script>
