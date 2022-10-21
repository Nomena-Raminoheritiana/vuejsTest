<script setup>

  import {onMounted} from "vue";
  import * as THREE from "three";
  import {gsap} from 'gsap'
  import {OrbitControls} from "three/addons/controls/OrbitControls";

  onMounted(() => {
    let camera,
        scene,
        element = document.getElementById('mercedes'),
        renderer,
        width = document.getElementById('mercedes-container').offsetWidth, // int || window.innerWidth
        height = 600, // int || window.innerHeight
        ratio = width / height;

    scene = new THREE.Scene();
    camera = new THREE.PerspectiveCamera(75, width/height, 0.1, 1000)
    renderer = new THREE.WebGLRenderer({
      antialias: true
    })
    renderer.setSize(width, height)
    renderer.setPixelRatio(ratio)
    element.appendChild(renderer.domElement)

    // creation sphere + texture
    const texture = new THREE.TextureLoader().load('./src/assets/mercedes.jpg')
    // on inverse notre image
    texture.wrapS = THREE.RepeatWrapping
    texture.repeat.x = -1
    const sphere = new THREE.Mesh(
        new THREE.SphereGeometry(50, 32, 32),
        new THREE.MeshBasicMaterial({
          // color: 0xff0000,
          map: texture,
          side: THREE.DoubleSide
        })
    )

    scene.add(sphere)

    // controllons le camera
    let control = new OrbitControls(camera, renderer.domElement)
    camera.position.set(-1,0,0)
    control.rotateSpeed = 0.2
    control.enableZoom = false
    control.autoRotate = true
    control.update()

    function animate()
    {
      requestAnimationFrame(animate)
      // sphere.rotation.y -= 0.001;
      // group.rotation.y = mouse.x * 0.5;
      // group.rotation.x = - mouse.y * 0.5;

      control.update()
      renderer.render(scene, camera)
    }

    animate()

    function onResize()
    {
      renderer.setSize(document.getElementById('mercedes-container').offsetWidth, height)
      camera.aspect = document.getElementById('mercedes-container').offsetWidth/height
      camera.updateProjectionMatrix()
    }

    document.addEventListener('resize', onResize)

  })
</script>

<template>
  <div class="position-relative w-100" id="mercedes-container">
    <div id="mercedes" class="mt-4 position-relative">
      <div id="log" class="position-absolute text-light"></div>
    </div>
  </div>

</template>

<style scoped>
  #vehicule {
    width:100%;
    height:auto
  }
  #vehiculeContainer {
    height: 600px !important;
    background: lightgrey;
  }
  #log {
    top:10px;
    left:10px
  }
</style>