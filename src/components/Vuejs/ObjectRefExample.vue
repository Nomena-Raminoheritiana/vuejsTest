<script setup>

import {ref} from "vue";

const ref1 = ref({count:1})

// une porté plus large que celle de la fonction reactive()
const incrementRef1 = (reference) => {
  ref1.value.count ++;
}

</script>


<template>
  <div class="mt-4 bg-light p-4 border">
    <h2 class="underline">Ref()</h2>
    <div>
      <small class="text-muted"><u>La limite de la fonction reactive()</u> </small><br>
      <ul>
        <li>const ref1 = ref({count:1})</li>
        <li>
          const incrementRef1 = (reference) => {
          ref1.value.count ++;
          }
        </li>
        <li>  @click="incrementRef1(ref1)</li>
      </ul>
      <span class="fw-bold">Référence A = {{ ref1.count }}</span>
    </div>
    <div class="mt-4">
      <button class="btn btn-sm border" @click="incrementRef1(ref1)">incrémenter la valeur de la reference</button>
    </div>

  </div>
</template>