<template lang="pug">
  #canvas
</template>

<script>

import 'three'
import { MTLLoader, OBJLoader } from 'three-obj-mtl-loader'

export default {
  data: () => ({
    $container: null,
    $scene: null,
    $renderer: null,
    $camera: null
  }),

  mounted () {
    // Set the scene size.
    const WIDTH = 400
    const HEIGHT = 300

    // Set some camera attributes.
    const VIEW_ANGLE = 45
    const ASPECT = WIDTH / HEIGHT
    const NEAR = 0.1
    const FAR = 10000

    // Get the DOM element to attach to
    this.$container = this.$el

    // Create a WebGL renderer, camera
    // and a scene
    this.$renderer = new THREE.WebGLRenderer()
    this.$camera =
      new THREE.PerspectiveCamera(
        VIEW_ANGLE,
        ASPECT,
        NEAR,
        FAR
      )

var pivot, mesh

    this.$scene = new THREE.Scene()
    const mtlLoader = new MTLLoader()
    const objLoader = new OBJLoader()

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

    mtlLoader.load('./assets/computer.mtl', (materials) => {
      materials.preload()
      objLoader.setMaterials(materials)
      objLoader.load('./assets/computer.obj', (obj => {
        pivot = new THREE.Object3D();
        obj.position.y = -10
        pivot.add(obj)
        this.$scene.add(pivot)
      }))
    })

    const animate = () => {
      requestAnimationFrame(animate)
      //cube.rotation.x += 0.05
      //cube.rotation.y += 0.05
      this.$renderer.render(this.$scene, this.$camera)
      if (pivot) {
        //pivot.rotation.x += 0.05
        pivot.rotation.y += 0.05
      }
    }
    animate()
  }
}
</script>
