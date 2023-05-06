<template>
  <v-app class="bg-grey-lighten-3 w-100">
    <div>
      <!--NAVIGATION BAR FROM REUSEABLE COMPONENT-->
      <Navbar />
    </div>
    <!--BODY -->
    <div class="mt-16 pa-16 text-center text-blue-grey-darken-3">
      <h2>What field do you want to practice for ?</h2>
    </div>
    <v-container class="d-flex justify-center align-center mt-12">
      <div>
        <!--reuseable component of STACK-->
        <Stacks :stacks="stacks" />
        <router-link to="/" class="link d-flex justify-center">
          <v-btn class="mt-10 bg-blue">Start Practicing</v-btn>
        </router-link>
      </div>
    </v-container>
  </v-app>
</template>
<script>
import Stacks from '../components/Stack.vue'
import Navbar from '../components/Navbar.vue'
export default {
  components: {
    Stacks,
    Navbar,
  },
  data() {
    return {
      stacks: [
        { title: 'Stack 1' },
        { title: 'Stack 2' },
        { title: 'Stack 3' },
        { title: 'Stack 4' },
        { title: 'Stack 5' },
        { title: 'Stack 6' },
        { title: 'Stack 7' }
      ]
    };
  },
};
</script>
<style>
.link {
  text-decoration: none;
}
</style>