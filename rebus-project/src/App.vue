<template>
  <div>
    <h1>
      {{ title }}
    </h1>
    <div v-if="showModal">
      <Modal :header="modal_header" :text="modal_text" :theme="modal_theme" @close="toggleModal"/>
    </div>
  </div>
</template>

<script>
import Modal from './components/Modal.vue'
// Root component
export default {
  name: 'App',
  components: {Modal},
  data() {
    return {
      title: '✨ Welcome to the Rebus Application ✨',
      modal_header: "La zia",
      modal_text: "la sa",
      modal_theme: "sale",
      showModal: true
    }
  },
  methods: {
    toggleModal() {
      this.showModal = !this.showModal
    }
  }
}
</script>

<!-- Global styles -->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
