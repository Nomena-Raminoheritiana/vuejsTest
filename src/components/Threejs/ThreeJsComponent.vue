<script setup>
import CubeThreeJs from "@/components/Threejs/CubeThreeJs.vue";
import EarthThreeJs from "@/components/Threejs/EarthThreeJs.vue";
import Mercedes from "@/components/Threejs/Mercedes.vue";
</script>

<template>
  <div class="green-sock-container mt-4 mb-5 bg-light p-4 border">
    <h2>ThreeJs Application + OrbitControl</h2>
    <CubeThreeJs />
    <EarthThreeJs />
    <Mercedes />
  </div>
</template>
