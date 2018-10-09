<template lang="pug">
  .home
    three-canvas
      
      sprite(name="room/tile-wall" :x="-2" :y="0" :z="0")
      sprite(name="room/tile" :x="-2" :y="0" :z="1")
      sprite(name="room/tile-corner" :x="-2" :y="0" :z="2")
      


      sprite(name="room/tile-wall" :x="-1" :y="0" :z="0" :rotate="0")
      sprite(name="room/tile" :x="0" :y="0" :z="0")
      sprite(name="room/tile-wall" :x="1" :y="0" :z="0" :rotate="180")

      sprite(name="room/tile-corner" :x="1" :y="0" :z="-1" :rotate="270")
      sprite(name="room/tile-wall" :x="0" :y="0" :z="-1" :rotate="270")
      sprite(name="room/tile-corner" :x="-1" :y="0" :z="-1")

      sprite(name="room/tile-corner" :x="1" :y="0" :z="1" :rotate="180")
      sprite(name="room/tile-wall" :x="0" :y="0" :z="1" :rotate="90")
      sprite(name="room/tile-corner" :x="-1" :y="0" :z="1" :rotate="90")

      //sprite(name="tile" :x="1" :y="1" :z="0")
      //sprite(name="tile" :x="2" :y="0" :z="0" :rotate="270")
      //sprite(name="tile" :x="0" :y="0" :z="0" :rotate="270")
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
