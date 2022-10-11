<template>
  <div class="green-sock-container mt-4 mb-5 bg-light p-4 border">
    <h2>GreenSocks Animation</h2>
    <hr>
    <div class="row mt-4">
      <div class="col-md-4">
        <h5 class="text-muted">Cliquer le box vert</h5>
        <small>Translation gauche - droite</small><br>
        <small class="text-primary"> <i><u>gsap.to('.box1', {  x: 200 })</u></i></small>
        <div class="box-green-container">
          <div class="box box1 green" @click="animerBoxVert"></div>
        </div>
      </div>
      <div class="col-md-4">
        <h5 class="text-muted">Cliquer le box rouge</h5>
        <small>Translation gauche - droite</small>
        <br>
        <small class="text-primary">
          <i>
            <u>
              gsap.fromTo( ".box2",{ x: 200, fill: 'blue'}, { x: 200, fill: 'green' });
            </u>
          </i>
        </small>
        <div class="box-green-container">
          <div class="box box2 red rounded-circle" @click="animerBoxRouge"></div>
        </div>
      </div>
      <div class="col-md-4">
        <h5 class="text-muted">Cliquer l'un des box</h5>
        <small>Translation gauche - droite</small>
        <br>
        <small class="text-primary">
          <i>
            <u>
              gsap.to([document.getElementById('carer'), document.getElementById('rond')], { x: 200 })
            </u>
          </i>
        </small>
        <div class="mt-5">
          <div class="box box3 green" id="carer" @click="animerDoubleBox"></div>
          <div class="box box3 mt-2 red rounded-circle" id="rond" @click="animerDoubleBox"></div>
        </div>
      </div>
    </div>
    <!-- Animation 2ème ligne -->
    <div class="row">
      <div class="col-md-4">
        <div class="mt-5">
          <small>Translation + rotation</small>
          <br>
          <small class="text-primary">
            <i>
              <u>
                gsap.to('.box4', {
                x: 200,
                rotation: 360,
                duration: 2,
                })
              </u>
            </i>
          </small>
          <div class="box box4 bg-primary mt-4" @click="animerBox4" id="carer" ></div>
        </div>
      </div>
      <div class="col-md-4">

      </div>
      <div class="col-md-4">

      </div>
    </div>
  </div>
</template>
<style scoped>
  .box-green-container {
    display: flex;
    align-items: center;
    justify-content: flex-start;
    min-height: 25vh;
    margin: 0;
    overflow: hidden;
  }

  .box {
    display: block;
    width:50px;
    height:50px;
    cursor: pointer
  }
  .green{
    background: green
  }
  .red {
    background: red
  }
</style>
<script>
  import {gsap} from 'gsap'

  export default {
   data() {
      return {
        boxVert: true,
        boxRouge: true,
        boxDouble: true,
        box4: true
      }
    },
    methods: {
      animerBoxVert()
      {
        const x = this.boxVert ? 200 : 0
        this.boxVert = !this.boxVert
        gsap.to('.box1', {
          x: x
        })
      },
      animerBoxRouge()
      {
        const xFrom = this.boxRouge ? 0 : 200
        const xTo = this.boxRouge ? 200 : 0
        this.boxRouge = !this.boxRouge
        gsap.fromTo( ".box2",{ x: xFrom, fill: 'blue'}, { x: xTo, fill: 'green' });
      },
      animerDoubleBox()
      {
        const x = this.boxDouble ? 200 : 0
        this.boxDouble = !this.boxDouble
        gsap.to([document.getElementById('carer'), document.getElementById('rond')], { x: x })
      },
      animerBox4() {
        const x = this.box4 ? 200 : 0
        const rotation = this.box4 ? 360 : -360
        this.box4 = !this.box4
        gsap.to('.box4', {
          x: x,
          rotation: rotation,
          duration: 2,
        })
      }
    }
    ,
    mounted() {

    }
  }
</script>