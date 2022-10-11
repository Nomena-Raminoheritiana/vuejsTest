<script setup>
import {nextTick, reactive} from "vue";

const state = reactive({
  count:0,
  objetProfond: {
    attr1: 'yes',
    attr2: true
  }
})

const increment = () => {
  state.count++
  nextTick(() => {
   console.log('Attendre la fin de mise à jour du DOM, ensuite ceci va être executé (nextTick)')
  })
}

const updateObjetprofond = () => {
 state.objetProfond .attr3 = 'test'
}
</script>
<template>

  <div class="mt-4 bg-light p-4 border">
    <h2 class="underline">Reactive()</h2>
    <div>
     1. Objet réactive en Vuejs : {{ state.count }}
      <span class="text-muted fs-6">(setup() const state = reactive({ count:0 }))</span>
    </div>
    <div>
      2. Objet réctive (json profond) : <span class="text-muted">{{ state.objetProfond }}</span>
    </div>
    <div class="mt-4">
      <button class="btn btn-sm border" @click="state.count = users.length">Cliquer ici pour actualiser le nombre des utilisateurs</button>
      <button class="btn btn-sm ms-2 border" @click="increment">Cliquer ici pour incrémenter le chiffre</button>
      <button class="btn btn-sm ms-2 border" @click="updateObjetprofond">Modifier le state 2. </button>
    </div>

  </div>
</template>
<script>
export default {
  props: {
    users: Array
  }
}
</script>