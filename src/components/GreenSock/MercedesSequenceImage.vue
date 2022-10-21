<template>
  <div class="mt-5 bg-dark p-3">
    <h3 class="text-white">Séquence d'image mercedes</h3>
    <h5 class="text-white">Scroller pour animer l'image</h5>
    <div class="imageSequenceContainer">
      <div class="imageSequenceSecondary">
        <canvas id="mercedesSequence"></canvas>
      </div>
    </div>
  </div>
</template>
<style scoped>
  .imageSequenceContainer {
    position:relative;
    height:100vh;
    overflow:auto
  }
  .imageSequenceSecondary {
    height: 8500px;
    position: relative;
  }
  #mercedesSequence {
    position:sticky;
    background: red !important;
    top:0px;
    left:0px;
    width:100%
  }

</style>
<script>
import {gsap} from 'gsap'
import ScrollTrigger from 'gsap/ScrollTrigger'
gsap.registerPlugin(ScrollTrigger);

export default {
  mounted() {
    const canvas = document.getElementById("mercedesSequence");
    const context = canvas.getContext("2d");

    canvas.width = 1600;
    canvas.height = 950;

    const frameCount = 107;
    const currentFrame = index => {
      return   './src/assets/mercedes_modeles/EQS-intro-'+(index + 1).toString().padStart(2, '0')+'.jpg'
    };

    const images = []
    const airpods = {
      frame: 0
    };

    for (let i = 0; i < frameCount; i++) {
      const img = new Image();
      img.src = currentFrame(i);
      images.push(img);
    }

    gsap.to(airpods, {
      frame: frameCount - 1,
      snap: "frame",
      ease: "none",
      scrollTrigger: {
        scrub: 0,
        scroller: '.imageSequenceContainer' // quand on scroll sur cet élément
      },
      onUpdate: render
    });
    gsap.set('canvas', {
      scale: 0.9
    })

    images[0].onload = render;

    function render() {
      context.clearRect(0, 0, canvas.width, canvas.height);
      context.drawImage(images[airpods.frame], 0, 0);
    }
  }
}
</script>