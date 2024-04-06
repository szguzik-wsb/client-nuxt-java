<script setup>
const route = useRoute();
const deleteArticle = async () => {
  try {
    await fetch('http://localhost:8080/articles/' + route.params.slug, {
      method: 'DELETE'
    });
    navigateTo('/articles')
  } catch (error) {
    console.error(error);
  }
}
</script>

<template>
    <section class="add_form">
      Czy na pewno chcesz skasować artykuł ?
      <button @click="deleteArticle">Tak</button>
      <button @click="navigateTo('/articles')">Nie</button>
    </section>

</template>