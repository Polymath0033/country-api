<template>
  <section>
    <div v-for="(country, index) in 8" :key="index" class="section">
      <div class="img"></div>
      <div class="text">
        <h4></h4>
        <div v-for="(fl, index) in 3" :key="index" class="flex">
          <h5></h5>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {};
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
.img {
  width: 100%;
  height: 100px;
  background-color: #dddddd;
}
.text {
  margin-top: 0.5rem;
  padding: 0.4rem;
}
.flex {
  display: flex;
  margin: 0.3rem;
  align-items: baseline;
  gap: 0.2rem;
}

.text h4 {
  width: 70%;
  margin-left: 0.2rem;
}
.flex h5 {
  width: 60%;
}
.text h4,
.flex h5 {
  background-color: #dddddd;
  padding: 1rem;
}
.img,
.text h4,
.flex h5 {
  background-image: linear-gradient(
    120deg,
    #dddddd 30%,
    #f0f0f0 38%,
    #f0f0f0 40%,
    #dddddd 48%
  );
  background-size: 200% 100%;
  background-position: 100% 0;
  animation: load 1s infinite;
}
@keyframes load {
  100% {
    background-position: -100% 0;
  }
}
@media screen and (max-width: 850px) {
  section {
    grid-template-columns: repeat(3, 1fr);
  }
}
@media screen and (max-width: 680px) {
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
