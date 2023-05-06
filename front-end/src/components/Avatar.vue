<template>
    <div class="mt-16">
        <v-avatar size="150" style="border: 2px solid black;">
            <v-img :src="profilePicUrl" />
            <v-icon class="icon" size="40" @click="$refs.fileInput.click()">mdi-camera</v-icon>
        </v-avatar>
        <v-file-input ref="fileInput" accept="image/*" v-model="profile_pic" @change="uploadProfilePic" hide-input label=""
            class="hidden-input">
        </v-file-input>
    </div>
</template>
<script>
import axiosInstance from 'axios';
export default {
    name: 'Avatar',
    data() {
        return {
            profilePicUrl: "", // replace with actual URL of user's profile picture
            profile_pic: "",
        };
    },
    methods: {
        async uploadProfilePic() {
            const formData = new FormData();
            formData.append('profile_pic', this.profile_pic);
            try {
                const response = await axiosInstance.post('register-update/', formData);
                this.profilePicUrl = response.data.profilePicUrl;
            } catch (error) {
                console.error(error);
            }
        }
    },
}
</script>
<style scoped>
.hidden-input {
    display: none;
}

.icon {
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
    z-index: 1;
}
</style>