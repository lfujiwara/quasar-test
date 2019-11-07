<template>
  <transition
    appear
    enter-active-class="animated zoomIn"
    leave-active-class="animated fadeOut"
  >
    <q-page class="flex flex-center">
      <q-card flat class="text-center">
        <div class="text-h3 q-pb-sm">
          CryptoWatcher
        </div>
        <div class="q-pb-lg">
          Built with Quasar CLI & Coinranking API
        </div>
        <q-btn to="/Watcher">
          Enter
        </q-btn>
      </q-card>
    </q-page>
  </transition>
</template>

<script>
export default {
  name: 'PageIndex'
}
</script>
