<template lang="pug">
  #canvas
    slot
</template>

<script>

import 'three'

export default {
  data: () => ({
    $container: null,
    $scene: null,
    $renderer: null,
    $camera: null,
    entities: [] //<-- array to hold items
  }),

  methods: {
    addEntity (entity) {
      // keep reference
      this.entities.push (entity)
      // add to scene
      this.$scene.add(entity)
    },
    removeEntity (entity) {
      console.log('remove!')
      this.entities = [ ...this.entities.filter(e => e !== entity) ]
    }
  },

  mounted () {
    // Set the scene size.
    const WIDTH = 400
    const HEIGHT = 300

    // Set some camera attributes.
    // const VIEW_ANGLE = 45
    // const ASPECT = WIDTH / HEIGHT
    // const NEAR = 0.1
    // const FAR = 10000

    // Get the DOM element to attach to
    this.$container = this.$el

    // Create a WebGL renderer, camera
    // and a scene
    this.$renderer = new THREE.WebGLRenderer()
   
    
    this.$scene = new THREE.Scene()

    var aspect = WIDTH / HEIGHT
    var d = 50;
    this.$camera = new THREE.OrthographicCamera( - d * aspect, d * aspect, d, - d, 1, 1000 );

    this.$camera.position.set( 20, 20, 20 ); // all components equal
    this.$camera.lookAt( this.$scene.position ); // or the origin

    /*this.$camera =
      new THREE.PerspectiveCamera(
        VIEW_ANGLE,
        ASPECT,
        NEAR,
        FAR
      )
    */

    var light = new THREE.AmbientLight( 0xffffff )

    this.$scene.add(light)

    this.$camera.position.z = 50

    // Add the camera to the scene.
    this.$scene.add(this.$camera)

    // Start the renderer.
    this.$renderer.setSize(WIDTH, HEIGHT)

    // Attach the renderer-supplied
    // DOM element.
    this.$container.appendChild(this.$renderer.domElement)

    const animate = () => {
      requestAnimationFrame(animate)
      //cube.rotation.x += 0.05
      //cube.rotation.y += 0.05
      this.$renderer.render(this.$scene, this.$camera)
    }
    animate()
  }
}
</script>
