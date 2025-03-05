<script setup lang="ts">
import CyberNav from '@/components/CyberNav.vue'
import { onMounted, onBeforeUnmount } from 'vue'
import * as THREE from 'three'

let renderer: THREE.WebGLRenderer
let scene: THREE.Scene
let camera: THREE.PerspectiveCamera
let particles: THREE.Points
let startTime: number
let colorPhase = 0

function initThree() {
  startTime = Date.now()
  // 创建渲染器
  renderer = new THREE.WebGLRenderer({
    antialias: true,
    alpha: true
  })
  renderer.setSize(window.innerWidth, window.innerHeight)
  document.querySelector('#app')?.appendChild(renderer.domElement)

  // 创建场景和相机
  scene = new THREE.Scene()
  camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000)
  camera.position.z = 30

  // 创建粒子几何体
  const geometry = new THREE.BufferGeometry()
  const vertices = []
  const colors = []
  for (let i = 0; i < 5000; i++) {
    const distance = Math.random() * 100
    const theta = Math.random() * Math.PI * 2
    const phi = Math.random() * Math.PI * 2
    
    vertices.push(
      distance * Math.sin(theta) * Math.cos(phi),
      distance * Math.sin(theta) * Math.sin(phi),
      distance * Math.cos(theta)
    )
    
    const color = new THREE.Color()
    color.setHSL(0.6, 1, 0.5 + distance / 200)
    colors.push(color.r, color.g, color.b)
  }
  geometry.setAttribute('position', new THREE.Float32BufferAttribute(vertices, 3))
  geometry.setAttribute('color', new THREE.Float32BufferAttribute(colors, 3))

  // 创建粒子材质
  const material = new THREE.PointsMaterial({
    size: 0.3,
    vertexColors: true,
    blending: THREE.AdditiveBlending,
    transparent: true,
    map: createCircleTexture(),
    alphaTest: 0.1
  })

  particles = new THREE.Points(geometry, material)
  scene.add(particles)
}

function createCircleTexture() {
  const canvas = document.createElement('canvas')
  canvas.width = 64
  canvas.height = 64
  
  const context = canvas.getContext('2d')
  if (!context) return new THREE.Texture()
  
  const centerX = canvas.width / 2
  const centerY = canvas.height / 2
  const radius = canvas.width / 3
  
  context.beginPath()
  context.arc(centerX, centerY, radius, 0, Math.PI * 2)
  context.fillStyle = '#ffffff'
  context.fill()
  
  const texture = new THREE.Texture(canvas)
  texture.needsUpdate = true
  return texture
}

function animate() {
  requestAnimationFrame(animate)
  
  const elapsedTime = (Date.now() - startTime) / 1000
  colorPhase = (elapsedTime * 0.1) % 1
  
  const colors = particles.geometry.attributes.color
  const positions = particles.geometry.attributes.position
  
  for (let i = 0; i < colors.count; i++) {
    const distance = Math.sqrt(
      positions.getX(i) ** 2 + 
      positions.getY(i) ** 2 + 
      positions.getZ(i) ** 2
    )
    
    const color = new THREE.Color()
    color.setHSL(
      (colorPhase + distance / 200) % 1,
      1,
      0.5 + distance / 200
    )
    
    colors.setXYZ(i, color.r, color.g, color.b)
  }
  colors.needsUpdate = true
  
  particles.rotation.x += 0.0005
  particles.rotation.y += 0.001
  renderer.render(scene, camera)
}

// 添加窗口大小变化监听器
function handleResize() {
  if (camera && renderer) {
    camera.aspect = window.innerWidth / window.innerHeight
    camera.updateProjectionMatrix()
    renderer.setSize(window.innerWidth, window.innerHeight)
  }
}

onMounted(() => {
  initThree()
  animate()

  // 添加窗口大小变化监听
  window.addEventListener('resize', handleResize)
})

onBeforeUnmount(() => {
  // 清理事件监听器
  window.removeEventListener('resize', handleResize)
})
</script>

<template>
  <CyberNav />
  <router-view />
</template>

<style>
#app canvas {
  position: fixed;
  top: 0;
  left: 0;
  z-index: -1;
}

.content-container {
  position: relative;
  z-index: 1;
  min-height: 100vh;
  overflow-y: visible;
  height: auto;
}

#app {
  font-family: 'Segoe UI', system-ui;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  position: relative;
  min-height: 100vh;
  overflow-y: visible;
}

.neon-text {
  color: #0ff;
  text-shadow: 0 0 10px #0ff;
  font-family: 'Orbitron', sans-serif;
}
</style>
