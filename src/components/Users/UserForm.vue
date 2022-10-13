<script setup>
defineProps({
  user: Object,
  update: Boolean
})
</script>
<template>
  <!-- Modal d'ajout -->
  <div class="modal fade" id="modal-add" tabindex="-1" aria-labelledby="ajoutUtilisateur" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h1 class="modal-title fs-5" id="exampleModalLabel">Formulaire d'un utilisateur </h1>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <form>
            <div class="row">
              <div class="col-md-6">
                <input type="text" class="form-control" placeholder="Entrer le nom" v-model="user.nom">
              </div>
              <div class="col-md-6">
                <input type="text" class="form-control" placeholder="Entrer le prénom"  v-model="user.prenom">
              </div>
            </div>
            <div class="mt-3">
              <input type="email" class="form-control" placeholder="exemple@gmail.com"  v-model="user.mail">
            </div>
            <div class="mt-3">
              <textarea class="form-control" rows="14" placeholder="Ajouter une biographie"  v-model="user.biographie"></textarea>
            </div>
          </form>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" id="close-modal" data-bs-dismiss="modal">Fermer</button>
          <button type="button" class="btn btn-primary" @click="update ? updateUser(user, true) : addUser()">Enregistrer</button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  emits: ['updateUser','addUser'],
  methods: {
    updateUser(user, submit) {
      this.$emit('updateUser',user, submit)
    },
    addUser() {
      this.$emit('addUser')
    }
  }
}
</script>