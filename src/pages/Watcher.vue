<template>
  <transition
    appear
    enter-active-class="animated fadeInRight"
    leave-active-class="animated fadeInLeft"
  >
    <div>
      <q-toolbar class="bg-primary text-white shadow-2">
        <q-btn flat round dense icon="arrow_back" class="q-mr-sm" to="/" />
        Back to landing page
      </q-toolbar>
      <div class="row justify-center">
        <CoinCard class="col-12 col-md-8"/>
      </div>
    </div>
  </transition>
</template>

<script>
import CoinCard from 'components/CoinCard.vue'
export default {
  components: {
    CoinCard
  }
}
</script>
