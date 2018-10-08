<script>
import { MTLLoader, OBJLoader } from 'three-obj-mtl-loader'

const mtlLoader = new MTLLoader()
const objLoader = new OBJLoader()

export default {
  props: {
    name: {
      type: String
    },
    x: {
      type: Number
    },
    y: {
      type: Number
    },
    z: {
      type: Number
    }
  },
  
  data: () => ({
    $sprite: null
  }),

  watch: {
    x () {
      this.$sprite.position.x = this.x
    },
    y () {
      this.$sprite.position.y = this.y
    },
    z () {
      this.$sprite.position.z = this.z
    }
  },
  
  created () {
    var pivot
    mtlLoader.load(`./assets/${this.name}.mtl`, (materials) => {
      materials.preload()
      objLoader.setMaterials(materials)
      objLoader.load(`./assets/${this.name}.obj`, (obj => {
        this.$sprite = new THREE.Object3D();
        obj.position.y = -10
        this.$sprite.position.x = this.x
        this.$sprite.position.y = this.y
        this.$sprite.position.z = this.z
        this.$sprite.add(obj)

        // add this entity to the parent scene
        this.$parent.addEntity(this.$sprite)
      }))
    })
  },

  render() {
    //return this.$scopedSlots.default({})
  },

  beforeDestroy () {
    console.log('destroy!!')
    this.$parent.removeEntity(this.$sprite)
  },

  destroyed () {
    console.log('show disapper!?')
    console.log('oh...')
  }
}
</script>
