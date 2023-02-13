<template>
  <section>
    <h1>
      {{ error }}
    </h1>
  </section>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Error",
  props: ["error"],
};
</script>

<style scoped>
section {
  display: flex;
  align-items: center;
  justify-content: center;
  position: fixed;
  width: 100%;
  height: 100%;
}
section h1 {
  color: red;
  font-weight: bold;
}
</style>
