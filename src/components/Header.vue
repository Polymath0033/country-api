<template>
  <header>
    <h3>Where in the world?</h3>
    <div class="mode">
      <i
        v-on:click="toggleTheme"
        :class="`${theme === 'dark' ? 'bi bi-moon' : 'bi bi-brightness-high'}`"
      ></i>
      <p>{{ theme }} mode</p>
    </div>
  </header>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Header",
  data() {
    return {
      theme: "light",
    };
  },
  methods: {
    toggleTheme() {
      const activeTheme = this.getTheme();
      if (activeTheme === "light") {
        this.setTheme("dark");
      } else {
        this.setTheme("light");
      }
    },
    setTheme(theme) {
      localStorage.setItem("theme", theme);
      this.theme = theme;
      document.documentElement.className = theme;
    },
    getMediaPreferenceScheme() {
      const darkPreference = window.matchMedia(
        "(prefers-color-scheme: dark)"
      ).matches;
      if (darkPreference) {
        return "dark";
      } else {
        return "light";
      }
    },
    getTheme() {
      return localStorage.getItem("theme");
    },
  },
  mounted() {
    const initTheme = this.getTheme() || this.getMediaPreferenceScheme();
    this.setTheme(initTheme);
  },
};
</script>

<style scoped>
header {
  position: fixed;
  display: flex;
  justify-content: space-between;
  padding: 1.5rem 2.5rem;
  box-shadow: 0 0 14px rgba(0, 0, 0, 0.2);
  background-color: var(--element);
  width: 100%;
  color: var(--text-primary);
  z-index: 100;
}
.mode {
  display: flex;
  gap: 0.4rem;
}
.mode p {
  text-transform: capitalize;
  color: var(--text-secondary);
}
i {
  color: var(--text-secondary);
  font-weight: bold;
}
</style>
