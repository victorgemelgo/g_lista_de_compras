<template>
  <div>
    <div class="row flex-center q-mt-lg">
      <q-btn
        icon="add"
        label="Criar nova lista"
        color="green-6"
        @click="goToNovaLista()"
        class="col-11"
      ></q-btn>
    </div>
    <div class="row flex-center">
      <q-card class="q-ma-lg col-xs-11 my-cart">
        <q-card-section>
          <h5 class="q-ma-xs">Titulo da minha lista</h5>
        </q-card-section>
        <hr />
        <q-card-section>
          <q-card-actions>
            <q-btn color="primary">Editar</q-btn>
            <q-btn color="red">Excluir</q-btn>
          </q-card-actions>
        </q-card-section>
      </q-card>
    </div>
  </div>
</template>

<script setup>
  defineOptions({
    name: 'HomeApp',
    methods: {
      goToNovaLista() {
        this.$router.push('/nova-lista');
      },
    },
  });
</script>

<style scoped>
  span {
    color: red;
  }
</style>
