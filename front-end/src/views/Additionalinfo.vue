<template>
  <div style="position: fixed; top: 0; left: 0; right: 0; bottom: 0; overflow-y: auto;">
    <div style="background-image: url('https://img.freepik.com/premium-vector/global-network-connection-concept-big-data-visualization-social-network-communication-global-computer-networks-internet-technology-business-science-vector-illustration_230610-825.jpg?w=1380');
       background-size: cover; height: 100vh; display: flex; justify-content: center; align-items: center;">
      <div class="w-50">
        <v-card class="elevation-24 ma-8">
          <v-card-title>
            <v-row align="center" justify="center">
              <v-col cols="12" md="8" lg="6">
                <h3 class="text-blue-grey-darken-3"> Provide us Additional Information</h3>
              </v-col>
            </v-row>
          </v-card-title>
          <v-row align="center" justify="center">
            <v-col cols="12" md="8" lg="6">
              <div class="profile">
                <v-row align="center" justify="center">
                  <v-col cols="12" md="8" lg="6">
                    <Avatar />
                  </v-col>
                </v-row>
              </div>
            </v-col>
          </v-row>
          <v-container>
            <v-text-field clearable label="Phone Number" type="tel" color="blue" variant="solo" v-model="phone"
              v-mask="'+## (###) ###-####'"></v-text-field>
            <v-select label="Designation" color="blue" variant="solo" :items="['Front-End', 'Back-End', 'Full Stack']"
              v-model="designation"></v-select>
            <v-text-field label="Years of Experiance" color="blue" variant="solo" type="number"
              v-model="experiance"></v-text-field>
            <v-select label="Interested In" color="blue" multiple variant="solo"
              :items="['Design', 'Integration', 'Database', 'Cloud', 'DevOps']" v-model="interest"></v-select>
            <div class="d-flex justify-content-center">
              <v-btn class="mb-8 mx-auto" color="blue" size="large" @click="additionalInfo">
                Submit
              </v-btn>
            </div>
          </v-container>
        </v-card>
      </div>
    </div>
  </div>
</template>
<script>
import axiosInstance from "../services/services.js";
import VueTheMask from 'vue-the-mask';
import Avatar from '../components/Avatar.vue';
import { toast } from "vue3-toastify";
import "vue3-toastify/dist/index.css";
export default {
  components: {
    Avatar,
  },
  data() {
    return {
      phone: "",
      designation: "",
      experiance: "",
      interest: "",
      fields: [],
    };
  },
  directives: { VueTheMask },
  methods: {
    additionalInfo() {
      const info = {
        email: this.$route.params.email,
        phone: this.phone,
        designation: this.designation,
        experiance: this.experiance,
        interest: JSON.stringify(this.interest),
      };
      axiosInstance
        .post("register-update/", info)
        .then((response) => {
          toast.success("Information added successfully", {
            transition: toast.TRANSITIONS.BOUNCE,
            position: toast.POSITION.TOP_RIGHT,
            autoClose: 2000,
          });
          console.log("Response from server:", response.data);
          this.$router.push({ path: `/login` });
        })
        .catch((error) => {
          console.log("Error from server:", error);
        });
      console.log("info", info);
    },
  },
};
</script>
<style scoped>
.profile {
  margin-bottom: 70px;
}
</style>