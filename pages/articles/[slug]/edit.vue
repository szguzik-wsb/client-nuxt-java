<script setup>
const route = useRoute();
const response = ref({});
const loading = ref(true)

const articleData = ref({
  id: null,
  title: null,
  content: null
});

onBeforeMount(async () => {
  const res = await fetch('http://localhost:8080/articles/' + route.params.slug);
  response.value = await res.json();
  console.log(response.value);

  articleData.value.title = response.value.title
  articleData.value.content = response.value.content
  articleData.value.id = route.params.slug

  loading.value = false


});

const updateArticle = async () => {
  try {
    const res = await fetch('http://localhost:8080/articles/' + route.params.slug, {
      method: 'PUT',
      headers: {
        'Content-Type': 'application/json'
      },
      body: JSON.stringify(articleData.value)
    });

    if (!res.ok) {
      throw new Error('Error while saving article');
    }

    const result = await res.json();
    console.log("Success", result);
    navigateTo('/articles')
  } catch (error) {
    console.error(error);
  }
}
</script>

<template>
  <Loader v-if="loading"></Loader>
  <template v-else>
    <section class="add_form">
      <h1>Edytuj artykuł</h1>
      <input type="text" v-model="articleData.title" placeholder="Tytuł">
      <textarea v-model="articleData.content" placeholder="Treść"></textarea>
      <button @click="updateArticle">Aktualizuj</button>
    </section>
  </template>
</template>

<style scoped lang="scss">
.add_form {
  width: 50%;
  display: flex;
  flex-direction: column;
  margin: 5px;
}
</style>