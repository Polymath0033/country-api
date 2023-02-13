<template>
  <Header />
  <router-view />
</template>
<script>
import Header from "./components/Header.vue";
export default {
  components: {
    Header,
  },
  data() {
    return {
      api: [],
    };
  },
  methods: {
    async getCountry() {
      try {
        const response = await fetch("https://restcountries.com/v2/all");
        if (!response.ok) {
          throw new Error("Failed to fetch countries");
        }
        const data = await response.json();
        this.api = [...data];
        return this.api;
      } catch (e) {
        throw new Error(e.message);
      }
    },
  },
  provide() {
    return {
      api: this.api,
      getCountry: this.getCountry,
    };
  },
  mounted() {
    this.getCountry();
  },
};
</script>
<style>
@import url("https://fonts.googleapis.com/css2?family=Nunito+Sans&display=swap");

*,
*::after,
*::before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Nunito Sans", sans-serif;
}
:root {
  --background: hsl(0, 0%, 98%);
  --text-primary: hsl(200, 15%, 8%);
  --element: hsl(0, 0%, 100%);
  --input: hsl(0, 0%, 52%);
  --text-secondary: hsl(0, 0%, 52%);
}
:root.dark {
  --background: hsl(207, 26%, 17%);
  --text-primary: hsl(0, 0%, 100%);
  --text-secondary: hsl(0, 0%, 88%);
  --element: hsl(209, 23%, 22%);
  --input: hsl(0, 0%, 98%);
}
body {
  background-color: var(--background);
}
#app {
  min-height: 100vh;
  background-color: var(--background);
}
</style>
