<script>
import { MTLLoader, OBJLoader } from 'three-obj-mtl-loader'

const mtlLoader = new MTLLoader()
const objLoader = new OBJLoader()

const TILE_SIZE = 30

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
    },
    rotate: {
      type: Number,
      default: 0
    }
  },
  
  data: () => ({
    $sprite: null,
    $bBoxHelper: null,
    $axisHelper: null,
    speed: 0.01
  }),

  watch: {
    x (nv, ov) {
      if (nv !== ov) this.setPosition()
    },
    y (nv, ov) {
      if (nv !== ov) this.setPosition()
    },
    z (nv, ov) {
      if (nv !== ov) this.setPosition()
    }
  },

  methods: {
    setPosition () {
      this.$sprite.position.x = this.x * TILE_SIZE
      this.$sprite.position.y = this.y * TILE_SIZE
      this.$sprite.position.z = this.z * TILE_SIZE
    }
  },

  methods: {
    animate () {
      
    }
  },
  
  created () {
    //declared once at the top of your code
    var axis = new THREE.Vector3(0,0.5,0);//tilted a bit on x and y - feel free to plug your different axis here
    //in your update/draw function
    

    var pivot
    mtlLoader.load(`./assets/${this.name}.mtl`, (materials) => {
      materials.preload()
      objLoader.setMaterials(materials)
      objLoader.load(`./assets/${this.name}.obj`, (obj => {
        this.$sprite = new THREE.Object3D();
        this.setPosition()
        // rad += radIncrement;
        obj.rotateOnAxis(axis,2)

        //this.$sprite.rotation.y = 3
        this.$sprite.add(obj)

        // add this entity to the parent scene
        this.$parent.addEntity(this.$sprite)

        this.$bBoxHelper = new THREE.BoundingBoxHelper(this.$sprite, 0x999999)
        this.$parent.$scene.add(this.$bBoxHelper)

        this.$axisHelper = new THREE.AxisHelper(18)
        this.$sprite.add(this.$axisHelper)

        var axis = new THREE.Vector3(0, 1, 0).normalize()
        if (this.$sprite) this.$sprite.rotateOnAxis(axis, (270 * Math.PI)/180)

      }))
    })
  },

  render() {
    return null
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
