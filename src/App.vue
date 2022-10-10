<script setup>
</script>

<template>
  <div class="container ">
    <h1 class="text-center anime-rotate mt-4">Test Animation & <span >Vuejs</span></h1>
    <button class="btn btn-primary scale-hover"
            id="btn-modal-user"
            data-bs-toggle="modal"
            data-bs-target="#modal-add"
            @click="initUserState()"
      >Ajouter un utilisateur</button>
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
    <div class="row">
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
              <a href="#" @click="deleteUser(user.id)" class="btn btn-danger btn-sm ms-2 anime-speed">Supprimer</a>
            </div>
          </div>
          <div class="card-footer text-muted">
            Contact : {{ user.mail }}
          </div>
        </div>
      </div>
    </div>
  </div>


<!--  <h1 @click="increments">{{ count }}</h1>-->
<!--  <header>-->
<!--    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />-->

<!--    <div class="wrapper">-->
<!--      <HelloWorld msg="You did it!" />-->
<!--    </div>-->
<!--  </header>-->

<!--  <main>-->
<!--    <TheWelcome />-->
<!--  </main>-->
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
  .anime-rotate {
    animation: combine-trans-rotate 2s infinite;
  }
  .scale-hover:hover {
    transform: scale(1.1);
    transition: all 0.5s ease-in;
  }
</style>
<script>
const userInitialState = {
  id: null,
  nom: '',
  prenom: '',
  mail: '',
  biographie: '',
  isActive: false,
}
export default {
  data() {
    return {
      user: {...userInitialState},
      users: [],
      update:false
    }
  },
  methods: {
    addUser() {
        this.user.id = this.users.length > 0 ? this.users.slice(-1)[0].id + 1 : 1
        this.users = [...this.users, this.user]
        this.user = userInitialState
        this.update = false
        closeUserFormModal()
    },
    updateUser(user, submit = false) {
      if(!submit) {
        openUserFormModal()
        let userFounded = this.users.find(userI => userI.id === user.id);
        this.user = {...userFounded}
        this.update = true
      } else {
        this.users = this.users.map((userA) => {
          if (userA.id === user.id) {
            return {...user}
          }
          return userA
        })
        closeUserFormModal()
      }
    },
    deleteUser(id) {
      this.users = this.users.filter((user) => user.id !== id)
    },
    initUserState() {
      this.user = {...userInitialState}
      this.update = false
    }
  },

  // `mounted` is a lifecycle hook which we will explain later
  mounted() {
   this.users = [
     {
       id: 1,
       nom: 'RAMINOHERITIANA',
       prenom: 'Nomena',
       mail: 'n.raminoheritiana@gmail.com',
       biographie: 'Le Lorem Ipsum est simplement du faux texte employé dans la composition et la mise en page avant impression. Le Lorem Ipsum est le faux texte standard de l\'imprimerie depuis les années 1500, quand un imprimeur anonyme assembla ensemble des morceaux de texte pour réaliser un livre spécimen de polices de texte. Il n\'a pas fait que survivre cinq siècles,',
       isActive: true,
     },
     {
       id: 2,
       nom: 'USER TEST 1 NOM',
       prenom: 'User 1 prénom',
       mail: 'n.test1@gmail.com',
       biographie: 'Le Lorem Ipsum est simplement du faux texte employé dans la composition et la mise en page avant impression. Le Lorem Ipsum est le faux texte standard de l\'imprimerie depuis les années 1500, quand un imprimeur anonyme assembla ensemble des morceaux de texte pour réaliser un livre spécimen de polices de texte. Il n\'a pas fait que survivre cinq siècles,',
       isActive: false,
     },
     {
       id: 3,
       nom: 'USER TEST 2 NOM',
       prenom: 'User 2 prénom',
       mail: 'n.test2@gmail.com',
       isActive: true,
       biographie: 'Le Lorem Ipsum est simplement du faux texte employé dans la composition et la mise en page avant impression. Le Lorem Ipsum est le faux texte standard de l\'imprimerie depuis les années 1500, quand un imprimeur anonyme assembla ensemble des morceaux de texte pour réaliser un livre spécimen de polices de texte. Il n\'a pas fait que survivre cinq siècles,',

     },
     {
       id: 4,
       nom: 'USER TEST 3 NOM',
       prenom: 'User 2 prénom',
       mail: 'n.test3@gmail.com',
       isActive: false,
       biographie: 'Le Lorem Ipsum est simplement du faux texte employé dans la composition et la mise en page avant impression. Le Lorem Ipsum est le faux texte standard de l\'imprimerie depuis les années 1500, quand un imprimeur anonyme assembla ensemble des morceaux de texte pour réaliser un livre spécimen de polices de texte. Il n\'a pas fait que survivre cinq siècles,',

     },
     {
       id: 5,
       nom: 'USER TEST 4 NOM',
       prenom: 'User 2 prénom',
       mail: 'n.test4@gmail.com',
       isActive: true,
       biographie: 'Le Lorem Ipsum est simplement du faux texte employé dans la composition et la mise en page avant impression. Le Lorem Ipsum est le faux texte standard de l\'imprimerie depuis les années 1500, quand un imprimeur anonyme assembla ensemble des morceaux de texte pour réaliser un livre spécimen de polices de texte. Il n\'a pas fait que survivre cinq siècles,',

     },
   ]
  }
}

const closeUserFormModal = () => {
  document.getElementById('close-modal').click()
}
const openUserFormModal = () => {
  document.getElementById('btn-modal-user').click()
}
</script>
