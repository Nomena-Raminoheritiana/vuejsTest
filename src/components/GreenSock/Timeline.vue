<template>
  <div>
    <div class="bg-dark">
      <div class="box-container mt-5" id="box-container">
        <h2 id="h2">Titre h2</h2>
        <div class="box-container-2" id="box-container-2">
          <div class="box bg-primary"></div>
          <div class="box bg-warning"></div>
          <div class="box bg-danger"></div>
          <div class="box bg-info"></div>
        </div>
      </div>
    </div>

    <div class="button-controls d-flex">
      <div class="m-auto">
        <button class="btn" @click.prevent="tm.restart()">demarrer l'animation </button>
        <button class="btn" @click.prevent="tm.pause()">pause</button>
        <button class="btn" @click.prevent="tm.resume()">resume</button>
        <button class="btn" @click.prevent="tm.reverse()">reverse</button>
        <button class="btn" @click.prevent="tm.play()">play</button>
      </div>
    </div>
  </div>
</template>
<style scoped>

  .button-controls {
    margin-top:20px
  }
  .button-controls button {
    margin-right: 12px
  }
  .box-container{
    display:flex;
    flex-direction: column;
    border: 1px solid black;
    padding:70px 50px;
    width:30vw;
    margin-left:auto;
    margin-right:auto;
    background: lightgrey;
  }
  .box-container-2 {
    display:flex;
    margin:auto;
    flex-direction: row !important;
  }
  h2 {
    margin:auto;
    margin-bottom:10px
  }

  .box {
    width:50px;
    height:50px;
    margin-right:5px;
  }

  button#animer {
    margin-top:20px
  }
</style>

<script>
  import {gsap} from 'gsap'
  import {ref} from "vue";

  export default {
    setup(){
      const tm = gsap.timeline({paused:true})
      return {
        tm
      }
    },
    data() {
      return {
        alreadyAnimed: false
      }
    },
    mounted() {
      this.tm.add(this.newAnimation_two())
      this.tm.add(this.newAnimation_one())
    }
    ,
    methods: {
      newAnimation_one() {
        const tm = gsap.timeline()
        tm.fromTo('#h2',{
          scale:1
        }, {
          scale:0.5
        })
            .fromTo('#h2', {
          scale:0.5,
        }, {
              scale:1.5,
              ease:'Power4.easeInOut'
            })
            .fromTo('#h2', {
              scale: 1.5
            }, {
              scale:1,
              ease:'Elastic.easeOut'
            })

        return tm
      },
      newAnimation_two() {
        const tm = gsap.timeline()
        tm.from('#box-container', {duration:1, opacity:0},)
            .from('#h2', {opacity:0, scale:0.8, ease:'back', onComplete:() => {
                console.log('animation h2 terminer')
              }},"+=0.5")
            .from('#box-container-2 div', {
              y:160,
              opacity:0,
              stagger: 0.5,
              duration:0.8,
              ease:'back',
              onComplete:() => {
                console.log('animation box terminer')
              }
            }, '<-0.4').yoyo(true)

        console.log(tm.totalDuration())
        tm.eventCallback(function() {
          console.log('animation terminé')
        })
        return tm;
      }
      ,
      animate() {
        this.tm.add(this.newAnimation_two())
        this.tm.add(this.newAnimation_one())
      }
    }
  }
</script>