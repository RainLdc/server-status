<template>
  <div>
    <v-app-bar color="primary" dark>
      <h1>{{appName}}</h1>
    </v-app-bar>
  </div>
</template>

<script>
export default {
  data: () => ({
    appName: process.env.APP_NAME || "Etat des Serveurs",
  }),
};
</script>
