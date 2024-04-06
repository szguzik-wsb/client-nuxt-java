<script setup>
const route = useRoute();
const response = ref({});
const loading = ref(true)

onBeforeMount(async () => {
  const res = await fetch('http://localhost:8080/articles/' + route.params.slug );
  response.value = await res.json();
  console.log(response.value);
  loading.value = false
});
</script>

<template>
  <Loader v-if="loading"></Loader>
  <template v-else>
    <h2> {{ response.title ?? '' }} </h2>
    <span> {{ response.content ?? '' }} </span>
  </template>
</template>

<style scoped>

</style>