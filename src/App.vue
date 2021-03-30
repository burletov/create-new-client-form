<template>
  <div class="main">
    <client-form></client-form>
  </div>
</template>

<script>
import ClientForm from './components/ClientForm.vue'

export default {
  data () {
    return {
      name: 'App'
    }
  },
  components: {
    'client-form': ClientForm
  }
}
</script>

<style lang="scss">
  @import "assets/theme";
</style>
