<template>
  <section>
    <div v-for="country in countries" :key="country.name" class="section">
      <router-link :to="country.name">
        <img :src="country.flag" :alt="country.name" />
      </router-link>

      <div class="text">
        <h4>{{ country.name }}</h4>
        <div class="flex">
          <h5>Population :</h5>
          <span>{{ country.population }}</span>
        </div>
        <div class="flex">
          <h5>Region :</h5>
          <span>{{ country.region }}</span>
        </div>
        <div class="flex">
          <h5>Capital :</h5>
          <span>{{ country.capital }}</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Section",
  props: ["countries"],
};
</script>

<style scoped>
section {
  padding-top: 2rem;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 3rem;
  position: relative;
  padding: 2rem;
}
.section {
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.4);
  background-color: var(--element);
}
.section img {
  width: 100%;
  height: 150px;
}
.text {
  padding: 1rem;
}
.text h4,
.flex h5 {
  color: var(--text-primary);
}
.flex span {
  color: var(--text-secondary);
  font-weight: bold;
}
.flex {
  display: flex;
  margin: 0.3rem;
  align-items: baseline;
  gap: 0.2rem;
}

@media screen and (max-width: 880px) {
  section {
    grid-template-columns: repeat(3, 1fr);
  }
}
@media screen and (max-width: 760px) {
  section {
    grid-template-columns: repeat(2, 1fr);
  }
}
@media screen and (max-width: 480px) {
  section {
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>
