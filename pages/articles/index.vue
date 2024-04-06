<script setup>
const response = ref({})
const loading = ref(true)

onBeforeMount(async () => {
  const res = await fetch('http://localhost:8080/articles')
  response.value = await res.json()
  console.log(response.value)
  loading.value = false
});
</script>

<template>
  <h1>Artykuły</h1> <br />
  <br>

  <NuxtLink to="/articles/add">[add]</NuxtLink>

  <br />
  <div class="wrapper">


    <Loader v-if="loading"></Loader>
    <template v-else>
      <div v-for="(value, index) in response" :key="index">
        <NuxtLink :to="'/articles/' + value.id">
          <h2>{{ index }} - {{ value.title }} </h2>
        </NuxtLink>

        <span>{{ value.content }}
          <NuxtLink :to="'/articles/' + value.id + '/edit'">[Edit]</NuxtLink>
          <NuxtLink :to="'/articles/' + value.id + '/delete'">[delete]</NuxtLink>
        </span>
        <hr />
      </div>
    </template>
  </div>
</template>

<style scoped lang="scss">


</style>