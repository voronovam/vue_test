<template>
  <div class="homePage">
    <Loader v-if="loading" />
    <template v-else>
      <div class="overlay"></div>
      <div class="modal">
        <PopupForm @closePopup="closePopup" />
      </div>
    </template>
  </div>
</template>

<script>
import PopupForm from '@/components/PopupForm.vue';
import Loader from '@/components/Loader';

export default {
  name: 'Home',
  data () {
    return {
      loading: true,
      visible: false
    }
  },
  components: {
    Loader,
    PopupForm
  },
  mounted() {
    setTimeout(() => {
      this.loading = false
    }, 3000);
  },
  methods: {
    closePopup () {
      this.loading = true;
    },
  }
}
</script>

<style scoped lang="sass">
.modal
  position: fixed
  top: 0
  left: 0
  width: 100%
  height: 100%
  overflow: hidden
  outline: 0
  z-index: 100
.overlay
  position: fixed
  top: 0
  left: 0
  width: 100vw
  height: 100vh
  background: rgba(#000, .5)
</style>