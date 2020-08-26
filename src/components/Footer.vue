<template>


  <v-footer color="primary" padless>
    <v-col class="text-center" cols="12">
      <a
        aria-label="Bouton-Liens"
        href="https://gitlab.com/leadrain"
        rel="noopener"
        target="_blank"
      >
        <img alt="Gitlab" src="../assets/gitlab.png" height="48" />
      </a>
      <a aria-label="Bouton-Liens" href="https://github.com/rainldc" rel="noopener" target="_blank">
        <img alt="Github" src="../assets/github.webp" height="48" />
      </a>
      <a
        aria-label="Bouton-Liens"
        href="https://www.linkedin.com/in/romain-le-duc/"
        rel="noopener"
        target="_blank"
      >
        <img alt="Linkedin" src="../assets/linkedin.png" height="48" class="ml-5" />
      </a>
    </v-col>
    <v-col class="primary lighten-1 py-4 text-center white--text" cols="12">
      {{ new Date().getFullYear() }} —
      <strong>Design by Romain LE DUC</strong>©
    </v-col>
  </v-footer>
</template>
