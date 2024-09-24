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
    <div class="row flex-center q-mt-md">
      <q-card class="my-card col-11">
        <q-card-section class="bg-primary text-white flex items-center justify-between">
          <div class="text-h6">Nome da Lista</div>
          <div class="text-subtitle2">00/00/00</div>
        </q-card-section>

        <q-card-actions class="flex justify-between">
          <q-btn
            flat
            icon="edit"
            color="primary"
          >
            Editar
          </q-btn>
          <q-btn
            flat
            icon="delete"
            color="red"
          >
            Excluir
          </q-btn>
        </q-card-actions>
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
