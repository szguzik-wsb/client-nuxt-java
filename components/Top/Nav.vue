<script setup>
</script>
<template>
  <div class="nav">
    <ul>
      <li>
        <NuxtLink to="/">Strona domowa</NuxtLink>
      </li>
      <li>
        <NuxtLink to="/about">o Nas</NuxtLink>
      </li>
      <li>
        <NuxtLink to="/articles">Artykuły</NuxtLink>
      </li>
      <li>
        <NuxtLink to="/contact">Kontakt</NuxtLink>
      </li>
    </ul>
  </div>
</template>
<style scoped lang="scss">
.nav {
  display: flex;
  width: auto;
  height: 40px;
  justify-content: center;
  @media (max-width: 288px) {
    height: 70px;
  }

  ul {
    display: inherit;
    flex-wrap: wrap;
    align-items: center;
    color: white;

    li {
      list-style-type: none;
      padding: 0 10px 0 10px;
      cursor: pointer;

      .router-link-active,
      .router-link-exact-active,
      a:hover {
        color: #ff0000;
      }
    }
  }
}
</style>