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
