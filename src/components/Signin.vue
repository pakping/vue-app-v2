<template>
  <v-container>
    <div v-if="loading" class="text-center">
      <v-progress-circular size="50" color="purple" indeterminate></v-progress-circular>
      <p>กำลังดำเนินการ...</p>
    </div>

    <v-card v-else :loading="loading" class="mx-auto my-12" max-width="374" elevation="2">
   <v-img
      height="250"
      src="https://cdn.vuetifyjs.com/images/cards/cooking.png"
    ></v-img>
      <v-card-title>Cafe-PakPing </v-card-title>
      <v-list>

        <v-list-item @click="signinByGoogle">
          <v-list-item-avatar>
            <v-icon color="red">mdi-google</v-icon>
          </v-list-item-avatar>
          <v-list-item-title>เข้าสู่ระบบด้วย Google</v-list-item-title>
        </v-list-item>
  
      </v-list>

    </v-card>
  </v-container>
</template>

<script>
import firebase from "firebase/app";
import "firebase/auth";

export default {
  data() {
    return {
      loading: true,
    };
  },

  mounted() {
    firebase
      .auth()
      .getRedirectResult()
      .then((result) => {
        if (result.user == null) {
          this.loading = false;
        } else {
          this.$router.replace("/");
        }
      });
  },

  methods: {
    signinByGoogle() {
      const provider = new firebase.auth.GoogleAuthProvider();
      firebase.auth().signInWithRedirect(provider);
    },
  },
};
</script>
