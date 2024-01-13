<template>
  <div>
    <h1>
      {{ title }}
    </h1>
    <RebusImage :imageSrc="imagePath" :hint="rebusHint" />
    <RebusSolution :words="rebusPattern"/>
  </div>
</template>

<script>
import Modal from './components/Modal.vue'
import RebusImage from './components/RebusImage.vue'
import RebusSolution from './components/RebusSolution.vue'

// Root component
export default {
  name: 'App',
  components: {RebusImage, RebusSolution},
  data() {
    return {
      title: '✨ Welcome to the Rebus Application ✨',
      imagePath: require('@/assets/rebuses/barbari.jpg'),
      rebusHint: 'Ce ne sono proprio tanti',
      rebusPattern: [
        { id: 1, letters: [{ id: 1, value: '' }, { id: 2, value: '' }, { id: 3, value: '' }] },
        { id: 2, letters: [{ id: 4, value: '' }, { id: 5, value: '' }, { id: 6, value: '' }] },
      ],
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
