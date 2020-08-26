<template>
  <div class="hello">
    <h1>Etat de servers</h1>
    <table class="table table-stripped table-hover" id="cont-table">
      <thead>
        <tr>
          <th>No.</th>
          <th>Name</th>
          <th>URL</th>
          <th>Port</th>
          <th>Status</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(site, index) in sites" :key="index">
          <td>{{ index + 1 }}</td>
          <td>{{ site.name }}</td>
          <td>
            <a v-bind:href="getHref(site)" target="_blank">{{ site.url }}</a>
          </td>
          <td>{{ site.port }}</td>
          <td v-if="site.status">
            <span class="label label-success">LIVE</span>
          </td>
          <td v-else>
            <span class="label label-danger">DOWN</span>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import json from "../assets/data.json";
export default {
  name: "HelloWorld",

  data() {
    return {
      siteDataUrl: json,
      sites: [],
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
