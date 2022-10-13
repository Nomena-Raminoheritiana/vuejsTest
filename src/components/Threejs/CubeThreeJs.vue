<script setup>
import * as THREE from 'three';
import {onMounted} from "vue";


onMounted(() => {
  const domThreejs = document.getElementById('threeJs');

  // moteur de rendu
  const renderer = new THREE.WebGLRenderer();
  renderer.setSize( domThreejs.clientWidth, domThreejs.clientHeight );
  domThreejs.appendChild(renderer.domElement)

  // camera
  const camera = new THREE.PerspectiveCamera( 70, domThreejs.clientWidth / domThreejs.clientHeight, 0.1, 1000 );
  camera.position.set( 0, 0, 5 );
  camera.lookAt( 0, 0, 0 );


  // on a besoin d'une scene
  const scene = new THREE.Scene();

  // on crée une box cube
  const geometry = new THREE.BoxGeometry( 1, 1, 1 );
  const material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
  const cube = new THREE.Mesh( geometry, material );
  scene.add( cube );

  const animate = () => {
    // créera une boucle qui animera notre cube à l'infini
    requestAnimationFrame( animate );
    cube.rotation.x += 0.01;
    cube.rotation.y += 0.01;
    renderer.render( scene, camera );
  }
  animate()

  // tracer un caré
  const materialLine = new THREE.LineBasicMaterial( { color: 0x0000ff } );
  const points = [];
  points.push( new THREE.Vector3( - 2, 0, 0 ) );
  points.push( new THREE.Vector3( 0, 2, 0 ) );
  points.push( new THREE.Vector3( 2, 0, 0 ) );
  points.push( new THREE.Vector3( 0, -2, 0 ) );
  points.push( new THREE.Vector3( -2, 0, 0 ) );
  const geometry2 = new THREE.BufferGeometry().setFromPoints( points );
  const line = new THREE.Line( geometry2, materialLine );
  scene.add( line );
  const animateLine = () => {
    // créera une boucle qui animera notre Line à l'infini
    requestAnimationFrame( animateLine );
    line.rotation.x += 0.05;
    renderer.render( scene, camera );
  }
  animateLine()

})

</script>

<template>
  <h6>Cube 3D</h6>
  <div class="threeJs position-relative" id="threeJs">
    <h2 class="position-absolute  text-light zIndex-10" id="text-threeJS">Texte au dessus</h2>
  </div>
</template>


<style scoped>
.threeJs {
  width: 100%;
  height: 750px;
  overflow: auto;
}
.zIndex-10 {
  z-index: 10 !important;
}
#text-threeJS {
  top: 2%;
  right:2%
}
</style>