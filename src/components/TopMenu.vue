<template>
    <div class="ui menu">
        <router-link to="/" class="item" active-class="active" exact>Home</router-link>
        <div class="right menu">
            <router-link to="/profile" class="item" active-class="active">Profile</router-link>
            <div v-if="currentUser" @click="signOut" class="link item">Sign Out</div>
            <router-link v-else to="/signin" class="item" active-class="active">Sign In</router-link>
        </div>
    </div>
</template>

<script>
import firebase from 'firebase'

export default {
  data: () => ({
    currentUser: null
  }),
  created () {
    firebase.auth().onAuthStateChanged((user) => {
      console.log('current user: ' + user)
      this.currentUser = user
    })
  },
  methods: {
    signOut () {
      firebase.auth().signOut()
      this.$router.replace('/')
    }
  }
}

</script>