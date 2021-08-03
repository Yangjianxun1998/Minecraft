<template>
  <div>
    <div id="container"></div>
  </div>
</template>
<script>
import * as THREE from 'three'
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'
export default {
  data () {
    return {
      renderer: null,
      mesh: null,
      controls: null,
      scene: null, // 渲染场景模型
      camera: null // 照相机
    }
  },
  mounted () {
    this.init()
    this.animate()
  },
  methods: {
    // 初始化
    init () {
      // 创建场景对象Scene
      this.setscene()
      // 设置数据
      this.setData()
      // 设置光源
      this.setlight()
      // 设置照相机
      this.setcamera()
      // 创建建渲染器
      this.setrender()
    },
    // 创建场景对象Scene
    setscene () {
      //  创建场景对象Scene
      this.scene = new THREE.Scene()
      // 辅助坐标系  参数250表示坐标系大小，可以根据场景大小去设置
      var axisHelper = new THREE.AxesHelper(10)
      this.scene.add(axisHelper)
      // GridHelper 是一个定义网格的对象。网格是二维线阵列
      const helper = new THREE.GridHelper(1, 30, 1, '#ffffff')
      this.scene.add(helper)
    },
    // 设置数据
    setData () {
      // 网格模型添加到场景中
      const geometry = new THREE.BoxGeometry(0.2, 0.2, 0.2)
      const material = new THREE.MeshNormalMaterial({})
      this.mesh = new THREE.Mesh(geometry, material)
      this.scene.add(this.mesh)
    },
    // 设置光源
    setlight () {},
    // 设置照相机
    setcamera () {
      // 相机设置
      const container = document.getElementById('container')
      const num = container.clientWidth / container.clientHeight
      this.camera = new THREE.PerspectiveCamera(70, num, 0.01, 10)
      this.camera.position.z = 1
    },
    // 创建渲染器对象
    setrender () {
      const container = document.getElementById('container')
      this.renderer = new THREE.WebGLRenderer({ antialias: true })
      this.renderer.setSize(container.clientWidth, container.clientHeight)
      container.appendChild(this.renderer.domElement)
      // 创建控件对象
      this.controls = new OrbitControls(this.camera, this.renderer.domElement)
    },
    // 动画
    animate () {
      requestAnimationFrame(this.animate)
      this.mesh.rotation.x += 0.01
      this.mesh.rotation.y += 0.02
      this.renderer.render(this.scene, this.camera)
    }
  }
}
</script>
<style>
#container {
  position: absolute;
  width: 100%;
  height: 100%;
}
</style>
