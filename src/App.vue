<template>
  <v-app>
    <vue-github-corners repo-url="https://github.com/algo-seacow/scoreboard" :bg-color="primary" />
    <router-view/>
  </v-app>
</template>

<script>
import { VueGithubCorners } from 'vue2-github-corners'

export default {
  name: "App",
  components: {
    VueGithubCorners
  },
  data() {
    return {
      primary: this.$vuetify.theme.themes.light.primary
    }
  },
  async created() {
    if (this.$router.currentRoute.name === "Index") {
      let user = localStorage.getItem("user")
      let repo = localStorage.getItem("repo")
      let gist = localStorage.getItem("gist")
      if (user && repo && gist)
        this.$router.push({
          name: "Scoreboard",
          query: {
            user: user,
            repo: repo,
            gist: gist
          }
        })
    }
    await this.github.initialize()
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
