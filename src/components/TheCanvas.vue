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
import { computed, defineProps, onMounted, ref, watch } from 'vue'

const { width, height } = useWindowSize()

const props = defineProps({
  someSize: Object
})

let controls

const aspectRatio = computed(() => width.value / height.value)

const experience = ref(null)
const scene = new Scene()
const camera = new PerspectiveCamera(75, aspectRatio.value, 0.1, 1000)
scene.add(camera)
const light = new DirectionalLight('hsl(0, 100%, 100%)')
const geometry = new BoxGeometry(0.05, 3, 3)
const material = new MeshStandardMaterial({
  side: FrontSide,
  color: 'hsl(0, 100%, 50%)',
  wireframe: false
})
scene.add(light)

const cube = new Mesh(geometry, material)

const floor = new Mesh(new BoxGeometry(3, 0.05, 3), material)
const wall = new Mesh(new BoxGeometry(3, 3, 0.05), material)
const axes = new AxesHelper(5)

scene.add(cube)
scene.add(floor)
scene.add(wall)
scene.add(axes)

light.position.set(0, 10, 10)
camera.position.set(5, 0, 5)
cube.position.set(0, 1.5, 1.5)
floor.position.set(1.5, 0, 1.5)
wall.position.set(1.5, 1.5, 0)

scene.background = new Color('hsl(0, 100%, 100%)')

let renderer

const animate = () => {
  renderer.render(scene, camera)
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
  console.log(props.someSize)
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
