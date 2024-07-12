<template>
  <v-app light>

    <Navbar v-if="!isLoginPage"/>
    <v-main>
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
export default {
  name: 'DefaultLayout',
  data () {
    return {
      title: 'Vuetify.js'
    }
  },
  computed: {
    // Determine if the current page is the login page
    isLoginPage() {
      return this.$route.path === '/login';
    },
    isDefault() {
      return this.$route.path === '/';
    },
  },
}
</script>
