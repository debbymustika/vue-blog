<template>
  <nav>
    <router-link to="/">Home</router-link> |
    <router-link to="/article">Artikel</router-link>
    <li class="nav-item" v-if="!isLoggedIn">
      <router-link class="nav-link" to="/login">Login</router-link>
      <router-link to="/register">Register</router-link>
    </li>
    <li class="nav-item" v-else>
      <button @click="logout" class="btn btn-link nav-link">Logout</button>
    </li>
  </nav>
  <router-view/>
</template>

<script>
  export default{
    data(){
      return{
        isLoggedIn:false
      };
    },
    created(){
      this.checkLoginStatus();
    },
    methods:{
      checkLoginStatus(){
        const user=JSON.parse(localStorage.getItem('user'));
        if(user && user.toker){
          this.isLoggedIn=true;
        }else{
          this.isLoggedIn=false;
        }
      },
      logout(){
        localStorage.removeItem('user');
        this.isLoggedIn=false;
        this.$router.push('/login');
      }
    }
  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
