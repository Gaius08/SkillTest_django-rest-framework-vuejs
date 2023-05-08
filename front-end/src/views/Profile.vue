<template>
    <v-app class="bg-grey-lighten-3 w-100">
        <!-- Navigation bar from reusable component -->
        <Navbar />
        <v-container>
            <v-row no-gutters>
                <v-col cols="4">
                    <v-card elevation="6" height="800" class="mt-16">
                        <v-row align="center" justify="center">
                            <v-col cols="12" md="8" lg="6">
                                <!-- Avatar component that displays user's profile picture -->
                                <Avatar />
                            </v-col>
                        </v-row>
                        <div class="mt-16">
                            <v-card-title>Profile Information</v-card-title>
                            <v-table dense>
                                <tbody>
                                    <!-- Table header -->
                                    <tr v-for="(item, index) in info" :key="index">
                                        <td>{{ item.field }}</td>
                                        <td>{{ item.value }}</td>
                                        <td><v-btn><i class="fa-solid fa-pen-to-square"></i></v-btn></td>
                                        <td><v-btn><i class="fas fa-save"></i></v-btn></td>
                                    </tr>
                                </tbody>
                            </v-table>
                        </div>
                    </v-card>
                </v-col>
                <!-- PREVIOUS SESSION -->
                <v-col cols="4">
                    <v-hover v-slot="{ isHovering, props }">
                        <v-card class="mt-16 ml-4" height="365" :elevation="isHovering ? 18 : 2"
                            :class="{ 'on-hover': isHovering }" v-bind="props">
                            <v-card-title>Previous Session</v-card-title>
                        </v-card>
                    </v-hover>
                    <!-- COMMENTS  -->
                    <v-hover v-slot="{ isHovering, props }">
                        <v-card class="mt-16 ml-4" height="365" :elevation="isHovering ? 18 : 2"
                            :class="{ 'on-hover': isHovering }" v-bind="props">
                            <v-card-title>Comments</v-card-title>
                        </v-card>
                    </v-hover>
                </v-col>
                <!-- UPCOMING SESSION -->
                <v-col cols="4">
                    <v-hover v-slot="{ isHovering, props }">
                        <v-card class="mt-16 ml-4" height="365" :elevation="isHovering ? 18 : 2"
                            :class="{ 'on-hover': isHovering }" v-bind="props">
                            <v-card-title>Upcoming Session</v-card-title>
                        </v-card>
                    </v-hover>
                    <!-- RATINGS -->
                    <v-hover v-slot="{ isHovering, props }">
                        <v-card class="mt-16 ml-4" height="365" :elevation="isHovering ? 18 : 2"
                            :class="{ 'on-hover': isHovering }" v-bind="props">
                            <v-card-title>Ratings</v-card-title>
                        </v-card>
                    </v-hover>
                </v-col>
            </v-row>
        </v-container>
    </v-app>
</template>
<script>
import Navbar from '../components/Navbar.vue';
import Avatar from '../components/Avatar.vue';
import axiosInstance from '../services/services';
export default {
    name: 'Profile',
    components: {
        Navbar,
        Avatar,
    },
    data() {
        return {
            info: [{
                field: "",
                value: ""
            }],
        }
    },
    created() {
        // Set authorization header for axios instance
        axiosInstance.defaults.headers.common['Authorization'] = `Token ${localStorage.getItem('token')}`;
        // Fetch user details from server
        axiosInstance.get('user-profile/')
            .then((response) => {
                this.info = [
                    {
                        field: 'First Name',
                        value: response.data.MyUser_serialized_data.first_name,
                    },
                    {
                        field: 'Last Name',
                        value: response.data.MyUser_serialized_data.last_name,
                    },
                    {
                        field: 'Email',
                        value: response.data.MyUser_serialized_data.email,
                    },
                    {
                        field: 'Phone',
                        value: response.data.UserProfileSerializer.phone,
                    },
                    {
                        field: 'Designation',
                        value: response.data.UserProfileSerializer.designation,
                    },
                    {
                        field: 'Experiance',
                        value: response.data.UserProfileSerializer.experiance,
                    },
                    {
                        field: 'Interest',
                        value: response.data.UserProfileSerializer.interest,
                    },
                ];
                console.log("res", response.data)
            })
            .catch((error) => {
                console.log(error);
            });
    },
};
</script>