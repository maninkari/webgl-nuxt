<template>
    <div ref="container"></div>
  </template>
  
  <script lang="ts">
  import * as THREE from 'three'
  
  export default {
    mounted() {
      const container = this.$refs.container as HTMLElement
  
      // Initialize the WebGL renderer
      const renderer = new THREE.WebGLRenderer()
    //   renderer.setSize(container.clientWidth, container.clientHeight)
      renderer.setSize(1000, 700)
      container.appendChild(renderer.domElement)
  
      // Create a new scene
      const scene = new THREE.Scene()
  
      // Add a camera to the scene
      const camera = new THREE.PerspectiveCamera(45, container.clientWidth / container.clientHeight, 1, 1000)
      camera.position.set(0, 0, 10)
      scene.add(camera)
  
      // Create a new mesh
      const geometry = new THREE.BoxGeometry()
      const material = new THREE.MeshBasicMaterial({ color: 0xff0000 })
      const mesh = new THREE.Mesh(geometry, material)
      scene.add(mesh)
  
      // Render the scene
      function render() {
        requestAnimationFrame(render)
        mesh.rotation.x += 0.01
        mesh.rotation.y += 0.01
        renderer.render(scene, camera)
      }
      render()
    }
  }
  </script>