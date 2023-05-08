<template>
  <v-app-bar scroll-behavior="fade-image elevate collapse hide" scroll-threshold="409"
    image="https://img.freepik.com/free-vector/pastel-ombre-background-pink-purple_53876-120750.jpg?w=1380&t=st=1683123380~exp=1683123980~hmac=2c4c1a31225b9f37f3c47d8bd9483deced5ed551b10b1f58b88ad636ddc7d46d">
    <v-app-bar-title> Interview Warmup </v-app-bar-title>
    <div>
      <router-link to="/help">
        <v-btn class="text-grey-darken-3" :class="{ 'active': $route.path === '/help' }">Home</v-btn>
      </router-link>
      <router-link to="/profile">
        <v-btn class="text-grey-darken-3" :class="{ 'active': $route.path === '/profile' }">Profile</v-btn>
      </router-link>
      <v-btn class="text-grey-darken-3" :class="{ 'active': $route.path === '/session' }">Session Attended</v-btn>
    </div>
    <v-avatar class="mr-8" size="x-large">
      <v-img src="https://cdn.vuetifyjs.com/images/john.jpg" class="" alt="profile picture"></v-img>
      <v-menu offset-y>
        <template #activator="{ on }">
          <v-icon v-on="on">mdi-dots-vertical</v-icon>
        </template>
        <v-list>
          <v-list-item @click="logout">Logout</v-list-item>
        </v-list>
      </v-menu>
    </v-avatar>
  </v-app-bar>
</template>
<script>
export default {
  name: 'Navbar',
  data() {
    return {
      avatarUrl: "",
    }
  },
  methods: {
    async logout() {
      try {
        // clear user data from local storage or state
        localStorage.removeItem("token");
        // redirect the user to the login page
        this.$router.push("/login");
        toast.success("Logged out successfully", {
          transition: toast.TRANSITIONS.BOUNCE,
          position: toast.POSITION.TOP_RIGHT,
          autoClose: 2000,
        });
      } catch (error) {
        console.error(error);
      }
    },
  },


}
</script>
  
  <!-- <style>
  .active {
    background-color: rgb(228, 28, 28);
    color: white;
  }
  </style> -->
  