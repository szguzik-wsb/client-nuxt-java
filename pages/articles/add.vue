<script setup>

const articleData = ref({
  id: null,
  title: null,
  content: null
});

const uniqueId = ref(0)
const nowIs = new Date();
nowIs.setMinutes(0)
nowIs.setSeconds(0)
nowIs.setMilliseconds(0)

const minisecondThisHour = Date.now() - nowIs.getTime();

onBeforeMount(() => {
  uniqueId.value = minisecondThisHour % (2 ** 31);
  console.log(uniqueId.value)
  articleData.value.id = uniqueId.value;
});

const saveArticle = async () => {
  try {
    const res = await fetch('http://localhost:8080/articles', {
      method: 'POST',
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
  } catch (error) {
    console.error(error);
  }
}
</script>
<template>
  <section class="add_form">
    <h1>Dodaj artykuł</h1>
    <input type="text" v-model="articleData.title" placeholder="Tytuł">
    <textarea v-model="articleData.content" placeholder="Treść"></textarea>
    <button @click="saveArticle">Zapisz</button>
  </section>

</template>

<style scoped lang="scss">
.add_form {
  width: 50%;
  display: flex;
  flex-direction: column;
  margin: 5px;
}
</style>