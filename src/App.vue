<script setup>
</script>

<template>
  <div class="container ">
    <h1 class="text-center anime-rotate mt-4">Test Animation & <span >Vuejs</span></h1>
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
              <a href="#" class="btn btn-primary btn-sm">Modifier</a>
              <a href="#" class="btn btn-danger btn-sm ms-2 anime-speed">Supprimer</a>
            </div>
          </div>
          <div class="card-footer text-muted">
            Contact : {{ user.mail }}
          </div>
        </div>
      </div>
    </div>
    <div class="mt-4">
      <h2>Formulaire utilisateur</h2>
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
    transition: all 0.5s;
    box-shadow: 0px 0px 10px #282828;
    z-index:10
  }
  .anime-rotate {
    animation: combine-trans-rotate 2s infinite;
  }
</style>
<script>
export default {
  data() {
    return {
      users: [
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
  },
  methods: {
    addUser(user) {
        this.users.push({
          id: this.users.slice(-1).id + 1,
          nom: user.nom,
          prenom: user.prenom,
          mail: user.mail,
          isActive: user.isActive
        })
    },
    updateUser(user) {
      let userFound = this.users.find(user => user.id === id);
      userFound = {
        id: this.users.slice(-1).id + 1,
        nom: user.nom,
        prenom: user.prenom,
        mail: user.mail,
        isActive: user.isActive
      }
    },
    deleteUser(id) {

    }
  },

  // `mounted` is a lifecycle hook which we will explain later
  mounted() {
    // `this` refers to the component instance.
    console.log(this) // => 1

    // data can be mutated as well
    this.count = 2
  }
}
</script>