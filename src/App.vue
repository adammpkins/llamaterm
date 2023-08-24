<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import GithubButton from 'vue-github-button'

</script>



<template>
    <header>
    <img alt="Vue logo" class="logo" src="@/assets/llama-md.png" width="125" height="125" />

    <div class="wrapper mb-10">
      <!-- <HelloWorld msg="You did it!" /> -->
      <div class="greetings text-center lg:text-left">
        <h3
          class="mb-10 font-extrabold text-transparent text-3xl bg-clip-text bg-gradient-to-r from-purple-400 to-pink-600">
          LlamaTerm</h3>
        <!-- Place this tag where you want the button to render. -->
        <github-button href="https://github.com/adammpkins/llama-terminal-completion"
          data-color-scheme="no-preference: dark; light: light; dark: dark;" data-icon="octicon-star"
          data-show-count="true" aria-label="Star adammpkins/llama-terminal-completion on GitHub">Star</github-button>
          <github-button  data-color-scheme="no-preference: dark; light: light; dark: dark;" href="https://github.com/adammpkins">Follow adammpkins</github-button>
        <github-button data-color-scheme="no-preference: dark; light: light; dark: dark;" href="https://github.com/adammpkins" data-icon="octicon-eye" data-show-count="true" aria-label="Watch adammpkins/llama-terminal-completion on GitHub">Watch</github-button>
        </div>

      <nav>
        <RouterLink to="/">HOME</RouterLink>
        <RouterLink to="/about">ABOUT</RouterLink>
        <RouterLink to="/docs">DOCS</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />

  
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}</style>
