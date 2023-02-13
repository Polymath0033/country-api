<template>
  <div v-for="ctr in country" :key="ctr.name">
    <section>
      <img :src="ctr.flag" :alt="ctr.name" />
      <aside class="aside">
        <div class="content">
          <h1>{{ ctr.name }}</h1>
          <div class="details">
            <div class="right">
              <div class="flex">
                <h5>Native Name:</h5>
                <span>{{ ctr.nativeName }}</span>
              </div>
              <div class="flex">
                <h5>Population:</h5>
                <span>{{ ctr.population }}</span>
              </div>
              <div class="flex">
                <h5>Region:</h5>
                <span>{{ ctr.region }}</span>
              </div>
              <div class="flex">
                <h5>Sub-Region:</h5>
                <span>{{ ctr.subregion }}</span>
              </div>
              <div class="flex">
                <h5>Capital:</h5>
                <span>{{ ctr.capital }}</span>
              </div>
            </div>
            <div class="left">
              <div class="flex">
                <h5>Top Level Domain:</h5>
                <span
                  v-for="(topLevelDomain, index) in ctr.topLevelDomain"
                  :key="index"
                  >{{ topLevelDomain }}</span
                >
              </div>
              <div class="flex">
                <h5>Currencies:</h5>
                <span v-for="(cur, index) in ctr.currencies" :key="index">{{
                  cur.name
                }}</span>
              </div>
              <div class="flex">
                <h5>Language:</h5>
                <span v-for="(language, index) in ctr.languages" :key="index">{{
                  language.name
                }}</span>
              </div>
            </div>
          </div>
          <div class="more-details">
            <h3>Borders Countries</h3>
            <div class="buttons">
              <button v-for="(borders, index) in ctr.borders" :key="index">
                {{ borders }}
              </button>
            </div>
          </div>
        </div>
      </aside>
    </section>
  </div>
</template>

<script>
export default {
  props: ["countries", "compute", "loading"],
  // eslint-disable-next-line vue/multi-word-component-names
  name: "country",
  data() {
    return {
      country: [],
    };
  },
  methods: {},
  mounted() {
    let c = [this.countries];
    for (const country of c) {
      this.country.push(country);
    }
  },
};
</script>

<style scoped>
section {
  margin-top: 3rem;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 3rem;
  align-items: center;
}
section img {
  width: 100%;
  height: 350px;
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.4);
}

.content {
  display: grid;
  gap: 2rem;
}
.details {
  display: flex;
  gap: 3rem;
}
.content h1 {
  color: var(--text-primary);
  /* margin-bottom: 1rem; */
}
.flex {
  display: flex;
  align-items: baseline;
  gap: 0.4rem;
  flex-wrap: wrap;
}
.flex h5 {
  color: var(--text-primary);
}
.flex span {
  color: var(--text-secondary);
}

.more-details {
  display: flex;
  gap: 1rem;
  width: 100%;
}
.more-details h3 {
  color: var(--text-primary);
}
.buttons button {
  all: unset;
  display: flex;
  color: var(--text-secondary);
  background-color: var(--element);
  box-shadow: 0 0 4px rgba(0, 0, 0, 0.4);
  padding: 0.2rem 1rem;
  align-items: center;
  font-weight: bold;
  justify-content: center;
}
.buttons {
  display: flex;
  gap: 1rem;
}
@media screen and (max-width: 800px) {
  section {
    grid-template-columns: 100%;
  }
  section img {
    height: 200px;
  }
  .details {
    flex-direction: column;
  }
  .more-details {
    display: grid;
  }
  .buttons {
    display: flex;
    gap: 1rem;
    width: 100%;
    justify-content: space-between;
  }
  .buttons button {
    width: 100%;
  }
}
</style>
