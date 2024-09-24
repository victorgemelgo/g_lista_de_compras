<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-toolbar-title>Lista de compras</q-toolbar-title>

        <q-btn
          icon="home"
          color="grey-2"
          text-color="primary"
          style="rounded"
          @click="goHome"
        />
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
  import { ref } from 'vue';

  defineOptions({
    name: 'MainLayout',
    methods: {
      goHome(){
        this.$router.push('/')
      }
    }
  });

  const leftDrawerOpen = ref(true);

  function toggleLeftDrawer() {
    leftDrawerOpen.value = !leftDrawerOpen.value;
  }
</script>
