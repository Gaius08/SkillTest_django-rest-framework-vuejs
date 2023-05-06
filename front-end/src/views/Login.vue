<template>
  <v-row sm="16" class="h-100h pa-16">
    <v-col cols="14" sm="16" md="18" class="w-100 elevation-24">
      <v-window v-model="step">
        <v-window-item :value="1">
          <v-row sm="16">
            <v-col cols="10" md="4" class="bg-orange-lighten-5">
              <v-card-text class="mt-12">
                <h2 class="text-center">Login </h2>
                <v-row align="center" justify="center">
                  <v-col cols="12" sm="10">
                    <v-form v-on:submit="submitForm">
                      <v-text-field label="Email" type="email" variant="outlined" color="teal" autocomplete="false"
                        class="mt-16 mb-2" v-model="email" :rules="emailRules" />
                      <v-text-field label="Password" variant="outlined" color="teal" autocomplete="false"
                        :rules="passwordRules" :append-inner-icon="showPassword ? 'mdi-eye-off' : 'mdi-eye'
                          " @click:append-inner="showPassword = !showPassword"
                        :type="showPassword ? 'text' : 'password'" v-model="password" />
                      <v-row>
                        <v-col cols="12" sm="7"> </v-col>
                        <v-col cols="12" sm="5" p="5px">
                          <!-- <span class="caption blue--text mt-n1">Forgot password</span> -->
                        </v-col>
                      </v-row>
                      <div class="text-center mt-2">
                        <v-btn @click="login" type="submit" color="teal" class="button">Log in</v-btn>
                      </div>
                      <h5 class="text-center grey--text mt-4 mb-3">
                        Or Log in using
                      </h5>
                      <div class="text-center">
                        <GoogleButton />
                      </div>
                      <v-card-text class="white--text">
                        <h5 class="text-center">Don't Have an Account Yet?</h5>
                      </v-card-text>
                      <div class="text-center">
                        <v-btn class="button" @click="step++">SIGN UP</v-btn>
                      </div>
                    </v-form>
                  </v-col>
                </v-row>
              </v-card-text>
            </v-col>
            <v-col cols="12" md="8" class="bg-light">
              <!-- Carousel -->
              <Carousel />
            </v-col>
          </v-row>
        </v-window-item>
        <v-window-item :value="2">
          <v-row>
            <v-col cols="12" md="8" class="bg-light">
              <!-- Carousel -->
              <Carousel />
            </v-col>
            <v-col cols="12" md="4" class="bg-orange-lighten-5">
              <v-card-text class="mt-12">
                <h2 class="text-center">Sign Up </h2>
                <v-row align="center" justify="center">
                  <v-col cols="12" sm="10">
                    <v-form v-on:submit="submitSignup">
                      <v-row>
                        <v-col cols="12" sm="6">
                          <v-text-field label="First Name" type="text" variant="outlined" color="teal "
                            autocomplete="false" class="mt-4 mb-2" v-model="firstname" :rules="nameRules" />
                        </v-col>
                        <v-col cols="12" sm="6">
                          <v-text-field label="Last Name" variant="outlined" color="teal" autocomplete="false"
                            class="mt-4 mb-2" v-model="lastname" :rules="nameRules" />
                        </v-col>
                      </v-row>
                      <v-text-field label="Email" variant="outlined" color="teal" autocomplete="false" class="mb-2"
                        v-model="email" :rules="emailRules" />
                      <v-text-field label="Password" variant="outlined" color="teal" autocomplete="false"
                        :rules="passwordRules" class="mb-2" :append-inner-icon="showPassword ? 'mdi-eye-off' : 'mdi-eye'
                          " @click:append-inner="showPassword = !showPassword"
                        :type="showPassword ? 'text' : 'password'" v-model="password" />
                      <v-text-field label="Confirm Password" variant="outlined" color="teal" autocomplete="false"
                        :rules="passwordRules" class="mb-2" :append-inner-icon="showPasswordComfirm ? 'mdi-eye-off' : 'mdi-eye'
                          " @click:append-inner="showPasswordComfirm = !showPasswordComfirm"
                        :type="showPasswordComfirm ? 'text' : 'password'" v-model="password2" />
                      <div class="text-center">
                        <v-btn color="teal" type="submit" class="button" @click="signup">Sign up</v-btn>
                      </div>
                      <h5 class="text-center grey--text mt-4 mb-3">
                        Or Sign up using
                      </h5>
                      <div class="text-center">
                        <GoogleButton />
                      </div>
                      <v-card-text class="white--text">
                        <h4 class="text-center">Already Signed up?</h4>
                      </v-card-text>
                      <div class="text-center">
                        <v-btn class="button" @click="step--">Log in</v-btn>
                      </div>
                    </v-form>
                  </v-col>
                </v-row>
              </v-card-text>
            </v-col>
          </v-row>
        </v-window-item>
      </v-window>
    </v-col>
  </v-row>
</template>
<script>
import axiosInstance from "../services/services.js";
import Carousel from "../components/Carousel.vue"
import GoogleButton from "../components/GoogleButton.vue"
import { toast } from "vue3-toastify";
import "vue3-toastify/dist/index.css";
export default {
  name: "Login",
  components: {
    Carousel,
    GoogleButton,
  },
  data() {
    return {
      step: 1,
      email: "",
      emailReg: "",
      password: "",
      password1: "",
      password2: "",
      firstname: "",
      lastname: "",
      showPassword: false,
      showPasswordComfirm: false,
      emailRules: [
        value => {
          if (value) return true
          return 'Password is requred.'
        },
        value => {
          if (/.+@.+\..+/.test(value)) return true
          return 'E-mail must be valid.'
        },
      ],
      emailRules: [
        value => {
          if (value) return true
          return 'E-mail is requred.'
        },
        value => {
          if (/.+@.+\..+/.test(value)) return true
          return 'E-mail must be valid.'
        },
      ],
      nameRules: [
        value => {
          if (value) return true
          return 'Name is requred.'
        },
        value => {
          if (value?.length <= 10) return true
          return 'Name must be less than 5 characters.'
        },
      ],
      passwordRules: [
        (value) => {
          if (!value) {
            return 'Password is required';
          } else if (value.length < 7) {
            return 'Password must be at least 7 characters long';
          } else if (!/[a-z]/.test(value)) {
            return 'Password must contain at least one lowercase letter';
          } else if (!/[A-Z]/.test(value)) {
            return 'Password must contain at least one uppercase letter';
          } else if (!/\d/.test(value)) {
            return 'Password must contain at least one number';
          } else if (!/[!@#$%^&*]/.test(value)) {
            return 'Password must contain at least one special character (!@#$%^&*)';
          } else {
            return true;
          }
        },
      ],
    };
  },
  methods: {
    signup() {
      const user = {
        username: this.firstname,
        first_name: this.firstname,
        last_name: this.lastname,
        email: this.email,
        password: this.password,
        password2: this.password2,
      };
      console.log(user);
      axiosInstance
        .post("register/", user)
        .then((response) => {
          toast.success("Your account has been created successfully", {
            transition: toast.TRANSITIONS.BOUNCE,
            position: toast.POSITION.TOP_RIGHT,
            autoClose: 2000,
          });
          this.$router.push({
            name: "Additionalinfo",
            params: { email: this.email },
          });
          console.log("Response from server:", response.data);
        })
        .catch((error) => {
          console.log("Error from server:", error);
        });
    },
    async login() {
      const user = {
        email: this.email,
        password: this.password,
      };
      console.log(user);
    },
    async submitForm(event) {
      // prevent the form from submitting
      event.preventDefault();
      // check if the fields are empty
      if (this.email === "" || this.password === "") {
        toast.error("Please enter both email and password", {
          transition: toast.TRANSITIONS.BOUNCE,
          position: toast.POSITION.TOP_RIGHT,
          autoClose: 2000,
        });
      } else {
        try {
          const response = await axiosInstance.post("login/", { email: this.email, password: this.password, });
          const token = response.data.access;
          // Save token in local storage
          localStorage.setItem("token", token);
          axiosInstance.defaults.headers.common[
            "Authorization"
          ] = `Bearer ${token}`;
          toast.success("Logged in successfully", {
            transition: toast.TRANSITIONS.BOUNCE,
            position: toast.POSITION.TOP_RIGHT,
            autoClose: 2000,
          });
          // Redirect to help page
          this.$router.push({ path: `/help` });
        } catch (error) {
          toast.error("Invalid User", {
            transition: toast.TRANSITIONS.BOUNCE,
            position: toast.POSITION.TOP_RIGHT,
            autoClose: 2000,
          });
          console.log("Error from server:", error);
        }
      }
    },
    submitSignup(event) {
      // prevent the form from submitting
      event.preventDefault();
      // check if the fields are empty
      if (
        this.email === "" ||
        this.password === "" ||
        this.firstname === "" ||
        this.lastname === ""
      ) {
        toast.error("Please fill all the field", {
          transition: toast.TRANSITIONS.BOUNCE,
          position: toast.POSITION.TOP_RIGHT,
          autoClose: 2000,
        });
      } else {
        const email = this.email;
        window.localStorage.setItem("email", email);

      }
    },
  },
};
</script>