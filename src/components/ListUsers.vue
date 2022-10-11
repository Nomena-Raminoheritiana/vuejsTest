<script setup>
defineProps({
  users: Array
})
</script>
<template>
  <div class="col-md-4 mt-5 " v-for="user in users">
    <div class="card anime-scale-in">
      <div class="card-header">
        <small class="text-uppercase fw-bold">{{ user.nom }}</small>
        <small class="text-capitalize ms-1 fst-italic">{{user.prenom}}</small>
      </div>
      <div class="card-body">
        <div>{{ user.biographie }}</div>
        <div class="mt-4">
          <a href="#" class="btn btn-primary btn-sm" @click="updateUser(user)">Modifier</a>
          <a href="#" @click="deleteUser(user)" class="btn btn-danger btn-sm ms-2 anime-speed">Supprimer</a>
        </div>
      </div>
      <div class="card-footer text-muted">
        Contact : {{ user.mail }}
      </div>
    </div>
  </div>
</template>
<style scoped>
.anime-speed:hover {
  animation: speedMove 0.5s infinite;
}
.anime-scale-in:hover {
  transform: scale(1.2);
  transition: all 0.4s ease-in;
  box-shadow: 0px 0px 10px #282828;
  z-index:10
}
</style>
<script>
export default {
  props: {
    users: Array
  },
  emits: ['suppression_user','modification_user'],
  methods: {
    deleteUser(user) {
      this.$emit('suppression_user',user)
    },
    updateUser(user) {
      this.$emit('modification_user',user)
    }
  }
}
</script>
