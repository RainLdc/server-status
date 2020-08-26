<template>
  <div red class="justify-center d-flex">
    <v-row justify="center">
      <img width="70px" height="70px" src="../assets/heartbeat.png" />
      <v-col cols="12">
        <v-data-table max-width="800px" :headers="headers" :items="sites" class="elevation-1">
          <template v-slot:item.status="{ item }">
            <v-chip :color="getColor(item.status)" dark>{{ item.status }}</v-chip>
          </template>
        </v-data-table>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import json from "../assets/data.json";
export default {
  name: "Status",

  data() {
    return {
      siteDataUrl: json,
      sites: [],
      headers: [
        { text: "Name", align: "start", value: "name" },
        { text: "URL", value: "url" },
        { text: "Port", value: "port" },
        { text: "Status", value: "status" },
      ],
    };
  },
  created: function () {
    this.loadData();
  },

  methods: {
    getHref: function (site) {
      if (!site.port) site.port = 80;
      return `https://${site.url}:${site.port}`;
    },

    loadData: function () {
      let self = this;
      self.sites = json;
      self.getStatus();
    },

    getColor(status) {
      if (status) return "green";
      else return "red";
    },

    getStatus: function () {
      let self = this;
      self.sites.forEach(function (site, index) {
        let url = `https://${site.url}`;
        if (site.port && site.port != 80 && site.port != 443)
          url += `:${site.port}`;

        fetch(url, { mode: "no-cors" }).then((resp) => {
          site.status = true;
          if (!resp.ok || resp.status != 200) site.status = false;
          if (resp.type == "opaque") site.status = true;
          self.$set(self.sites, index, site);
        });
      });
    },
  },
};
</script>
