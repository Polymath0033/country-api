<template>
  <main>
    <div class="header">
      <div class="search">
        <input
          type="search"
          name="search"
          id="search"
          placeholder="Search for  a country"
          v-model.trim="search"
        />
        <i class="bi bi-search"></i>
      </div>

      <div class="tab">
        <button v-on:click="toggleTab" class="tab-btn">
          Filter by region
          <i :class="tab === false ? 'bi bi-caret-down' : 'bi bi-caret-up'"></i>
        </button>
        <div class="buttons" v-show="tab">
          <button
            v-for="(region, index) in [
              'Africa',
              'Americas',
              'Asia',
              'Europe',
              'Oceania',
            ]"
            :key="index"
            v-on:click="toggleRegion(region)"
          >
            {{ region }}
          </button>
        </div>
      </div>
    </div>
    <div v-if="loading">
      <countries-loading></countries-loading>
    </div>
    <div v-if="countries.length === 0 && loading === false" class="not-found">
      <h1>Not Found !!!</h1>
    </div>
    <Section :countries="countries" />
  </main>
</template>

<script>
import Section from "../components/Section";
import CountriesLoading from "../components/UI/CountriesLoading";
export default {
  components: {
    Section,
    CountriesLoading,
  },
  inject: ["getCountry"],
  data() {
    return {
      region: "",
      tab: false,
      api: [],
      search: "",
      loading: false,
      error: null,
    };
  },
  methods: {
    toggleTab() {
      this.tab = !this.tab;
    },
    toggleRegion(region) {
      this.region = region;
      this.tab = false;
    },
    async country() {
      try {
        this.loading = true;
        let countries_ = await this.getCountry();
        this.api = [...countries_];
        this.loading = false;
      } catch (e) {
        this.loading = false;
        this.error = e.message;
      }
    },
  },
  computed: {
    countries() {
      const african = this.api.filter((country) => country.region === "Africa");
      const americas = this.api.filter(
        (country) => country.region === "Americas"
      );
      const asia = this.api.filter((country) => country.region === "Asia");
      const europe = this.api.filter((country) => country.region === "Europe");
      const oceania = this.api.filter(
        (country) => country.region === "Oceania"
      );

      let country =
        this.region === ""
          ? this.api
          : this.region === "Africa"
          ? african
          : this.region === "Americas"
          ? americas
          : this.region === "Asia"
          ? asia
          : this.region === "Europe"
          ? europe
          : this.region === "Oceania"
          ? oceania
          : this.api;
      return country.filter((search) => search.name.includes(this.search));
    },
  },
  mounted() {
    this.country();
  },
};
</script>

<style scoped>
main {
  position: relative;
  /* padding: 2rem; */
  top: 74px;
}
.not-found {
  display: flex;
  justify-content: center;

  width: 100%;
  color: var(--text-primary);
}
.header {
  display: flex;
  justify-content: space-between;
  width: 100%;
  padding: 2rem;
}
.search {
  position: relative;
  width: 35%;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.4);
  display: flex;
  align-items: center;
  background-color: var(--element);
  border-radius: 4px;
}
.search input {
  width: 100%;
  padding: 0.5rem 1rem 0.5rem 2rem;
  border: none;
  outline: none;

  background-color: var(--element);
  color: var(--text-secondary);
  font-weight: bold;
  display: flex;
  align-items: center;
}
.search i {
  position: absolute;
  z-index: 1000;
  top: 5px;
  font-weight: bold;
  left: 5px;
  color: var(--input);
  font-size: 1.2rem;
}
.tab {
  position: relative;
}
.tab-btn,
.buttons {
  all: unset;
  display: flex;
  justify-content: space-between;
  color: var(--text-secondary);
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.4);
  padding: 0.5rem 1rem;
  background-color: var(--element);
  border-radius: 5px;
  width: 90%;
}
.buttons {
  position: absolute;
  color: var(--text-secondary);
  display: flex;
  flex-direction: column;
  margin-top: 0.1rem;
  z-index: 100000;
  border-radius: 5px;
}
.buttons button {
  all: unset;
  padding: 0.5rem 1rem;
  background: var(--element);
}
@media screen and (max-width: 680px) {
  .header {
    flex-direction: column;
    gap: 1rem;
  }
  .search {
    width: 100%;
  }
  .buttons,
  .tab-btn {
    width: 45%;
  }
}
</style>
