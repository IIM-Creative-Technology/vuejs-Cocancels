<template>
    <div id="nav">
        <router-link v-for="user in this.$store.state.users" :key="user" v-show="user.isConnected"  to="/admin">Gérer le blog</router-link>
        <div  v-for="user in this.$store.state.users" :key="user" v-show="user.isConnected" class="navSeparateLinks"></div>
        <router-link to="/blog">Blog</router-link>
        <div class="navSeparateLinks" ></div>
        <!-- <router-link v-for="user in this.$store.state.users" :key="user" v-show="user.isConnected == false" to="/login">Login</router-link> -->
        <!-- <div v-if="user == undefined ||user.username"> -->
          <router-link v-if="!this.$store.state.userConnected" to="/login">Login</router-link>
      <!-- </div> -->
        <a class="deconnexion" v-for="user in this.$store.state.users" :key="user" v-show="user.isConnected" @click="deconnexion(user)">Déconnexion</a>

    </div>
    <router-view/>
</template>

<script>
export default {
  name: 'Navbar',

  data: function() {
        return {
            user : this.user,
            userConnected : this.$store.state.userConnected
        }      
    },

  methods: {
    deconnexion(user){
      console.log(this.$store.state.userConnected)
      this.$store.commit("DECONNEXION", user)
      console.log(this.$store.state.userConnected)
    },
  }

}
</script>
<style>
  #nav{
    display: flex;
    align-items: center;
  }
  #nav a{
    padding: 0px 10px 0px 10px;
    text-decoration: none;
  }
  #nav .navSeparateLinks{
    background-color: #000;
    height: 15px;
    width: 2px;
  }

  .deconnexion:hover{
    cursor: pointer;
    color: red;
  }

</style>
