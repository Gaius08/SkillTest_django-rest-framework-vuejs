<template>
     <v-app class="bg-grey-lighten-3 w-100">
    <div>
        <Navbar />
    </div>
    <div class="mt-16">
        <v-checkbox label="Audio Check"></v-checkbox>
        <v-checkbox label="Video Check"></v-checkbox>
        <v-checkbox label="Screen Share"></v-checkbox>
    </div>
</v-app>
</template>
<script>
import Navbar from '../components/Navbar.vue'
export default {
    name : 'System Check',
    components : {
        Navbar,
    }
    
}
</script>