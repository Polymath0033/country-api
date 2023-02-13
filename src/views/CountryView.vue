<template>
  <main>
    <button class="back" v-on:click="back">
      <h2><i class="bi bi-arrow-left"></i></h2>
      back
    </button>
    <div v-if="error">
      <Error :error="error" />
    </div>
    <div v-if="loading">
      <country-loading></country-loading>
    </div>

    <Country v-else :countries="api" />
  </main>
</template>

<script>
import Country from "../components/Country";
import CountryLoading from "../components/UI/CountryLoading";
import Error from "../components/Error";
export default {
  name: "country-view",
  components: {
    Country,
    CountryLoading,
    Error,
  },
  inject: ["getCountry"],
  data() {
    return {
      api: [],
      name: "",
      loading: false,
      error: null,
    };
  },
  methods: {
    back() {
      this.$router.go(-1);
    },
    async country() {
      try {
        this.loading = true;
        let c = await this.getCountry();
        const id = this.$route.params.name;
        let country = [...c];
        const ap = country.find((ap) => ap.name === id);
        this.api = ap;
        this.loading = false;
      } catch (e) {
        this.loading = false;
        console.log(e);
        this.error = e.message;
      }
    },
  },

  mounted() {
    this.country();
  },
  created() {
    this.name = this.$route.params.name;
  },
};
</script>

<style scoped>
main {
  position: relative;
  top: 74px;
  padding: 2rem;
}
.back {
  all: unset;
  display: flex;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.3);
  width: 25%;
  /* padding: 0.4rem; */
  background: var(--element);
  color: var(--text-secondary);
  font-weight: bold;
  text-transform: capitalize;
  align-items: center;
  justify-content: center;
  gap: 1rem;
  height: 2rem;
}
.back i {
  font-weight: bold;
  /* font-size: 2rem; */
}
@media screen and (max-width: 680px) {
  .back {
    width: 50%;
  }
}
</style>
