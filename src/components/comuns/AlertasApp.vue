<template>
  <q-banner
    id="alerta"
    inline-actions
    :class="bgClass"
  >
    {{ texto }}
  </q-banner>
</template>

<script>
  export default {
    name: 'AlertasApp',
    props: {
      texto: {
        type: String,
        required: true,
      },
      status: {
        type: String,
        required: true,
      },
    },
    computed: {
      bgClass() {
        switch (this.status) {
          case 'erro':
            return 'text-white bg-negative text-center';
          case 'alerta':
            return 'text-white bg-warning text-center';
          case 'sucesso':
            return 'text-white bg-positive text-center';
          default:
            return 'text-white bg-positive';
        }
      },
    },
  };
</script>

<style scoped>
  #alerta {
    margin: 10px 0 10px 0;
  }
</style>
