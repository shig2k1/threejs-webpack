<script>
import { MTLLoader, OBJLoader } from 'three-obj-mtl-loader'

const mtlLoader = new MTLLoader()
const objLoader = new OBJLoader()

const TILE_SIZE = 3

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
    axis: null,
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
    },
    rotate (nv, ov) {
      if (nv !== ov) this.setRotation()
    }
  },

  methods: {
    setPosition () {
      this.$sprite.position.x = (this.x * TILE_SIZE) - 1.5
      this.$sprite.position.y = this.y * TILE_SIZE
      this.$sprite.position.z = (this.z * TILE_SIZE) - 1.5
    },
    setRotation () {
      if (this.$sprite && this.rotate) this.$sprite.rotateOnAxis(this.axis, (this.rotate * Math.PI)/180)
    },
    animate () {
      
    }
  },
  
  created () {
    //declared once at the top of your code
    this.axis = new THREE.Vector3(0,1,0);//tilted a bit on x and y - feel free to plug your different axis here
    //in your update/draw function
    

    var pivot
    mtlLoader.load(`./assets/${this.name}.mtl`, (materials) => {
      materials.preload()
      objLoader.setMaterials(materials)
      objLoader.load(`./assets/${this.name}.obj`, (obj => {
        this.$sprite = new THREE.Object3D();
        
        this.setPosition()

        obj.scale.set(0.1, 0.1, 0.1)

        //this.$sprite.rotation.y = 3
        this.$sprite.add(obj)

        // add this entity to the parent scene
        this.$parent.addEntity(this.$sprite)

        /*this.$bBoxHelper = new THREE.BoxHelper(this.$sprite, 0x999999)
        this.$parent.$scene.add(this.$bBoxHelper)

        this.$axisHelper = new THREE.AxesHelper(18)
        this.$sprite.add(this.$axisHelper)
        */
        this.setRotation()
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
