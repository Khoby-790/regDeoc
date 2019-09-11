<template>
  <v-app>
    <v-app-bar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Med Register</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
    </v-app-bar>

    <v-content>
      <RegisterForm />
    </v-content>
  </v-app>
</template>

<script>
import RegisterForm from "./components/RegisterForm";

export default {
  name: "App",
  components: {
    RegisterForm
  },
  data: () => ({
    //
  })
};
</script>
