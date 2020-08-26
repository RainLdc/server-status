<template>
  <v-app>
    <Menu />
    <v-main>
      <Status />
    </v-main>
    <Footer/>
  </v-app>
</template>

<script>
import Status from "./components/Status";
import Menu from "./components/Menu";
import Footer from "./components/Footer";

export default {
  name: "App",

  components: {
    Status,
    Menu,
    Footer
  },
};
</script>
