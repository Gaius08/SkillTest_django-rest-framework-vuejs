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
    <v-container class="d-flex justify-center align-center mt-4">
      <div>
        <div>
          <v-row v-for="(stack, index) in stacks" :key="index">
            <v-hover v-slot="{ isHovering, props }" open-delay="0">
              <v-btn class="mt-4 list" :elevation="isHovering ? 16 : 2"
                :class="{ 'active': activeIndex === index, 'on-hover': isHovering }" @click="setActive(index)" v-bind="props">
                <h3>{{ stack.technology_name }}</h3>
              </v-btn>
            </v-hover>
          </v-row>
        </div>
        <router-link to="/" class="link d-flex justify-center">
          <v-btn class="mt-10 bg-blue">Start Practicing</v-btn>
        </router-link>
      </div>
    </v-container>
  </v-app>
</template>
<script>
import Navbar from '../components/Navbar.vue'
import axiosInstance from '../services/services';
export default {
  components: {
    Navbar,
  },
  data() {
    return {
      activeIndex: "",
      stacks: [],
      selectedStacks: []
    };
  },
  created() {
    axiosInstance.defaults.headers.common['Authorization'] = `Token ${localStorage.getItem('token')}`;
    axiosInstance.get('pref-tech/')
      .then(response => {
        this.stacks = response.data.techObject_serializer
        console.log("kk", response.data.techObject_serializer)
      })
      .catch(error => {
        console.log(error);
      })
  },
  methods: {
    setActive(index) {
      this.activeIndex = index
    },
  }
};
</script>
<style scoped>
.link {
  text-decoration: none;
}
.list {
  width: 400px;
}
.list:hover {
  background-image: linear-gradient(to bottom right, #eb87d5, #86baee);
}
.active {
  background-image: linear-gradient(to bottom right, #eb87d5, #86baee);
  color: white;
}
</style>