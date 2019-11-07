<template>
  <q-layout view="lHh Lpr lFf">
    <q-page-container>
      <router-view />
    </q-page-container>
    <CreditsFooter/>
  </q-layout>
</template>

<style>
body {
  font-family: 'Montserrat';
}
</style>

<script>
import CreditsFooter from 'components/CreditsFooter.vue'
export default {
  name: 'MyLayout',
  components: {
    CreditsFooter
  }
}
</script>
