<script setup>
import { useWindowSize } from '@vueuse/core'
import {
  AxesHelper,
  Color,
  DirectionalLight,
  FrontSide,
  Mesh,
  MeshBasicMaterial,
  MeshStandardMaterial,
  PerspectiveCamera,
  Scene,
  BoxGeometry,
  WebGLRenderer
} from 'three'
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js'
import { computed, onMounted, ref, watch } from 'vue'

const { width, height } = useWindowSize()

console.log(width, height)

let controls

const aspectRatio = computed(() => width.value / height.value)

const experience = ref(null)
const scene = new Scene()
const camera = new PerspectiveCamera(75, aspectRatio.value, 0.1, 1000)
scene.add(camera)
const light = new DirectionalLight('hsl(0, 100%, 100%)')
const geometry = new BoxGeometry(1, 1, 1)
const material = new MeshStandardMaterial({
  side: FrontSide,
  color: 'hsl(0, 100%, 50%)',
  wireframe: false
})
scene.add(light)

const cube = new Mesh(geometry, material)
const axes = new AxesHelper(5)

scene.add(cube)
scene.add(axes)

light.position.set(0, 0, 10)
camera.position.z = 5

scene.background = new Color('hsl(0, 100%, 100%)')

let renderer

const animate = () => {
  renderer.render(scene, camera)
  cube.rotation.y += 0.01
  controls.update()
  requestAnimationFrame(animate)
}

onMounted(() => {
  renderer = new WebGLRenderer({
    antialias: true,
    canvas: experience.value
  })
  controls = new OrbitControls(camera, renderer.domElement)
  controls.enableDamping = true
  renderer.setSize(width.value, height.value)

  updateCamera()
  updateRenderer()
  renderer.render(scene, camera)
  animate()
})

function updateCamera() {
  camera.aspect = aspectRatio.value
  camera.updateProjectionMatrix()
}

function updateRenderer() {
  renderer.setSize(width.value, height.value)
  renderer.setPixelRatio(window.devicePixelRatio)
}

watch(aspectRatio, updateRenderer)
watch(aspectRatio, updateCamera)
</script>
<template>
  <canvas ref="experience" />
</template>
