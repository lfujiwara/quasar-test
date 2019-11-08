<template>
  <transition
    appear
    enter-active-class="animated zoomIn"
    leave-active-class="animated fadeOut"
  >
    <q-page class="flex flex-center">
      <q-card flat class="text-center full-width">
        <div class="text-h4">
          CryptoWatcher
        </div>
        <div class="q-mt-sm">
          Built with Quasar CLI & Coinranking API
        </div>
        <div class="row justify-center">
          <StatsCarousel class="q-mt-xl col-12 col-md-5"/>
        </div>
        <q-btn to="/Watcher" class="q-mt-md">
          Enter
        </q-btn>
      </q-card>
    </q-page>
  </transition>
</template>

<script>
import StatsCarousel from '../components/StatsCarousel.vue'
export default {
  name: 'PageIndex',
  components: {
    StatsCarousel
  }
}
</script>
