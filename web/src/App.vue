<template>
  <v-app>
    <TopToolbar></TopToolbar>
    <v-content>
      <router-view></router-view>
    </v-content>
    <BottomNav></BottomNav>
    <v-snackbar
        :value="successMessage"
        app
        bottom
        color="success"
        elevation="20"
    >
      {{ successMessage }}
    </v-snackbar>

    <v-snackbar
        :value="errorMessage"
        app
        bottom
        color="error"
        elevation="20"
    >
      {{ errorMessage }}
    </v-snackbar>
  </v-app>
</template>

<script>
import TopToolbar from "@/components/TopToolbar";
import BottomNav from "@/components/BottomNav";


function initStore(store) {
  store.dispatch('FETCH_SUBSCRIPTIONS');
  store.dispatch("FETCH_COLLECTIONS");
}

export default {
  components: {
    TopToolbar,
    BottomNav
  },

  created() {
    this.$vuetify.theme.dark = false;
    this.$vuetify.theme.themes.dark.primary = '#0899ab';
    this.$vuetify.theme.themes.light.primary = '#d73964';

    initStore(this.$store);
  },

  computed: {
    successMessage() {
      return this.$store.state.successMessage;
    },
    errorMessage() {
      return this.$store.state.errorMessage;
    }
  },

  watch: {
    successMessage() {
      setTimeout(() => {
        this.$store.commit("SET_SUCCESS_MESSAGE", "");
      }, 1000);
    },
    errorMessage() {
      setTimeout(() => {
        this.$store.commit("SET_ERROR_MESSAGE", "");
      }, 1000);
    }
  }
}
</script>
<style>
@import "css/app.css";
</style>