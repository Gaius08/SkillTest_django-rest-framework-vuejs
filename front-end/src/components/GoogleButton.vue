<template>
    <div>
      <v-btn color="white" dark class="mb-2" @click="signInWithGoogle">
        <img src="../assets/Google/google-logo-png-29532.png" alt="Google logo" class="mr-2 google-logo">
        Sign in with Google
      </v-btn>
    </div>
  </template>
  
  <script>
  export default {
    methods: {
      signInWithGoogle() {
        // Handle Google sign-in logic here
      },
    },
  };
  </script>
  
  <style scoped>
  .google-logo {
    width: 20px;
    height: 20px;
  }
  </style>