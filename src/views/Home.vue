<template lang="pug">
  .home
    three-canvas
      sprite(name="computer" :x="1" :y="0" :z="0")
      sprite(name="box" :x="20" :y="0" :z="0")
      sprite(name="box" :x="20" :y="0" :z="20")
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import ThreeCanvas from '@/components/ThreeCanvas.vue'
import Sprite from '@/components/Sprite.vue'

export default {
  name: 'home',
  components: {
    HelloWorld,
    ThreeCanvas,
    Sprite
  }
}
</script>
