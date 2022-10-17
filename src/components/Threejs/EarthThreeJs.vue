<script setup>

  import {onMounted} from "vue";
  import * as THREE from "three";
  import {gsap} from 'gsap'

  onMounted(() => {
    let camera,
        scene,
        element = document.getElementById('sphere'),
        renderer,
        width = document.getElementById('sphere-container').offsetWidth, // int || window.innerWidth
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

    // creation sphere
    const sphere = new THREE.Mesh(
        new THREE.SphereGeometry(5, 50, 50),
        new THREE.MeshBasicMaterial({
          // color: 0xff0000,
          map: new THREE.TextureLoader().load('./src/assets/earth-uv-map.jpg')
        })
    )

    // creation des étoiles
    const starPos = []
    for (let i=0; i<=10000; i++){
      const x = (Math.random() - 0.5) * 2000
      const y = (Math.random() - 0.5) * 2000
      const z = - Math.random() * 2000
      starPos.push(x,y,z)
    }

    const starGeometry =  new THREE.BufferGeometry()
    starGeometry.setAttribute('position', new THREE.Float32BufferAttribute(starPos, 3))
    const stars = new THREE.Points(
       starGeometry,
        new THREE.PointsMaterial({
          color: 0xffffff
        })
    )
    scene.add(stars)

    const group = new THREE.Group()
    group.add(sphere)
    scene.add(group)

    camera.position.z = 10


    const mouse = {
      x:0,
      y:0
    }

    function animate()
    {
      requestAnimationFrame(animate)
      sphere.rotation.y -= 0.001;
      // group.rotation.y = mouse.x * 0.5;
      // group.rotation.x = - mouse.y * 0.5;
      gsap.to(group.rotation, {
        y: mouse.x * 0.5,
        x: - mouse.y * 0.5,
        duration: 2
      })
      renderer.render(scene, camera)
    }

    animate()


    element.addEventListener('mousemove', function(e) {
      mouse.x = (e.clientX / width) *2 - 1
      mouse.y = - (e.clientY / height) *2 + 1

    })
  })
</script>

<template>
  <div class="position-relative w-100" id="sphere-container">
    <div id="sphere" class="mt-4 position-relative">
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