<script setup>
import ListUsers from './components/Users/ListUsers.vue'
import UserForm from './components/Users/UserForm.vue'
import Loading from './components/Loading.vue'
import ObjectReactiveExample from './components/Vuejs/ObjectReactiveExample.vue'
import {userInitialState} from './components/constants/initialState'
import GreenSock from "./components/GreenSock/GreenSock.vue";
import ObjectRefExample from "./components/Vuejs/ObjectRefExample.vue";
import ThreeJsComponent from "@/components/Threejs/ThreeJsComponent.vue";
</script>

<template>
  <div class="container ">
    <h1 class="text-center anime-rotate mt-4">Test Animation & <span >Vuejs</span></h1>
    <ThreeJsComponent />
    <button class="btn btn-primary scale-hover"
            id="btn-modal-user"
            data-bs-toggle="modal"
            data-bs-target="#modal-add"
            @click="initUserState()"
      >Ajouter un utilisateur</button>
    <UserForm :user="user" :update="update" @addUser="addUser" @updateUser="updateUser"/>
    <div class="row">
      <Loading v-if="loading" />
      <ListUsers v-if="!loading" v-bind:users="users" @suppression_user="deleteUser" @modification_user="updateUser"/>
    </div>
    <div class="row">
      <div class="col-md-6">
        <ObjectReactiveExample :users="users" />
      </div>
      <div class="col-md-6">
        <ObjectRefExample />
      </div>
    </div>
    <GreenSock />
  </div>
</template>

<style scoped>
  .anime-rotate {
    animation: combine-trans-rotate 2s infinite;
  }
  .scale-hover:hover {
    transform: scale(1.1);
    transition: all 0.5s ease-in;
  }
</style>
<script>
export default {
  data() {
    return {
      user: {...userInitialState},
      users: [],
      update:false,
      loading: true
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
    deleteUser(userPayload) {
      this.users = this.users.filter((user) => user.id !== userPayload.id)
    },
    initUserState() {
      this.user = {...userInitialState}
      this.update = false
    }
  },

  // `mounted` is a lifecycle hook which we will explain later
  mounted() {
    // simulation requete API (on va dire que le chargement des donn??es prend 2s )
    setTimeout(() => {
      this.users = [
        {
          id: 1,
          nom: 'RAMINOHERITIANA',
          prenom: 'Nomena',
          mail: 'n.raminoheritiana@gmail.com',
          biographie: 'Le Lorem Ipsum est simplement du faux texte employ?? dans la composition et la mise en page avant impression. Le Lorem Ipsum est le faux texte standard de l\'imprimerie depuis les ann??es 1500, quand un imprimeur anonyme assembla ensemble des morceaux de texte pour r??aliser un livre sp??cimen de polices de texte. Il n\'a pas fait que survivre cinq si??cles,',
          isActive: true,
        },
        {
          id: 2,
          nom: 'USER TEST 1 NOM',
          prenom: 'User 1 pr??nom',
          mail: 'n.test1@gmail.com',
          biographie: 'Le Lorem Ipsum est simplement du faux texte employ?? dans la composition et la mise en page avant impression. Le Lorem Ipsum est le faux texte standard de l\'imprimerie depuis les ann??es 1500, quand un imprimeur anonyme assembla ensemble des morceaux de texte pour r??aliser un livre sp??cimen de polices de texte. Il n\'a pas fait que survivre cinq si??cles,',
          isActive: false,
        },
        {
          id: 3,
          nom: 'USER TEST 2 NOM',
          prenom: 'User 2 pr??nom',
          mail: 'n.test2@gmail.com',
          isActive: true,
          biographie: 'Le Lorem Ipsum est simplement du faux texte employ?? dans la composition et la mise en page avant impression. Le Lorem Ipsum est le faux texte standard de l\'imprimerie depuis les ann??es 1500, quand un imprimeur anonyme assembla ensemble des morceaux de texte pour r??aliser un livre sp??cimen de polices de texte. Il n\'a pas fait que survivre cinq si??cles,',

        },
        {
          id: 4,
          nom: 'USER TEST 3 NOM',
          prenom: 'User 2 pr??nom',
          mail: 'n.test3@gmail.com',
          isActive: false,
          biographie: 'Le Lorem Ipsum est simplement du faux texte employ?? dans la composition et la mise en page avant impression. Le Lorem Ipsum est le faux texte standard de l\'imprimerie depuis les ann??es 1500, quand un imprimeur anonyme assembla ensemble des morceaux de texte pour r??aliser un livre sp??cimen de polices de texte. Il n\'a pas fait que survivre cinq si??cles,',

        },
        {
          id: 5,
          nom: 'USER TEST 4 NOM',
          prenom: 'User 2 pr??nom',
          mail: 'n.test4@gmail.com',
          isActive: true,
          biographie: 'Le Lorem Ipsum est simplement du faux texte employ?? dans la composition et la mise en page avant impression. Le Lorem Ipsum est le faux texte standard de l\'imprimerie depuis les ann??es 1500, quand un imprimeur anonyme assembla ensemble des morceaux de texte pour r??aliser un livre sp??cimen de polices de texte. Il n\'a pas fait que survivre cinq si??cles,',

        },
      ];
      this.loading = false
    },2000)

  }
}

const closeUserFormModal = () => {
  document.getElementById('close-modal').click()
}
const openUserFormModal = () => {
  document.getElementById('btn-modal-user').click()
}
</script>
