<template>
     <v-app class="bg-grey-lighten-3 w-100">
    <div>
        <Navbar />
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
