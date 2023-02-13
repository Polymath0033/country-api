<template>
  <section>
    <div class="img"></div>
    <div class="aside">
      <div class="content">
        <h1></h1>
        <div class="details">
          <div class="left">
            <div v-for="(fl, index) in 5" :key="index" class="flex">
              <h5></h5>
            </div>
          </div>
          <div class="right">
            <div v-for="(fl, index) in 4" :key="index" class="flex">
              <h5></h5>
            </div>
          </div>
        </div>
        <div class="more-details">
          <h3></h3>
          <div class="buttons">
            <button v-for="(btn, index) in 3" :key="index"></button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {};
</script>

<style scoped>
/* * {
  background: var(--background);
} */
:root {
  --background: linear-gradient(
    120deg,
    #dddddd 30%,
    #f0f0f0 38%,
    #f0f0f0 40%,
    #dddddd 48%
  );
}
section {
  margin-top: 3rem;
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 3rem;
  align-items: center;
}
.img {
  width: 100%;
  height: 350px;
  background: var(--background);
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
  width: 250px;
  padding: 1.5rem;
  background: var(--background);

  /* margin-bottom: 1rem; */
}

.flex h5 {
  background: var(--background);
  padding: 1rem;
  width: 200px;
  margin-top: 0.4rem;
}

.more-details {
  display: flex;
  gap: 1rem;
  width: 100%;
}
.more-details h3 {
  background: var(--background);
  padding: 1rem;
  width: 100px;
}
.buttons button {
  all: unset;
  width: 30%;
  background: var(--background);
}
.buttons {
  display: flex;
  gap: 1rem;
  width: 50%;
}
.img,
.content h1,
.buttons button,
.more-details h3,
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
@media screen and (max-width: 680px) {
  section {
    grid-template-columns: 100%;
  }
  .img {
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
    padding: 1rem;
  }
}
</style>
