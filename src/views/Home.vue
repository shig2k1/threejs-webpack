<template lang="pug">
  .home
    three-canvas
      sprite(name="tile" :x="1" :y="0" :z="0")
      sprite(name="tile" :x="2" :y="0" :z="0" :rotate="270")
      //sprite(name="room/tm" :x="2" :y="0" :z="0" :rotate="90")
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
