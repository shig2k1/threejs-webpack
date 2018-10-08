<template lang="pug">
  .home
    three-canvas
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import ThreeCanvas from '@/components/ThreeCanvas.vue'

export default {
  name: 'home',
  components: {
    HelloWorld,
    ThreeCanvas
  }
}
</script>
