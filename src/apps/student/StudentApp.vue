<template>
<div class="h-screen mainpage flex justify-center items-center font-snig text-base">
    <Navigation v-if="$route.name !== 'exp' & $route.name !== 'exam'"/>
    
    <router-view/>
</div>
</template>

<script>
import { mapGetters } from 'vuex'
import axios from 'axios'

import Navigation from './components/Navigation.vue'

export default {
    name: 'StudentApp',
    components: {
        Navigation
    },
    computed: {
        ...mapGetters('auth', [
            'isAuthenticated',
            'token',
            'user'
        ])
    },
    created() {
        this.$store.commit('auth/INIT')
        axios.defaults.headers.common['Authorization'] = 'Token ' + this.token
        this.$store.dispatch('auth/getUser')
    },
}
</script>
