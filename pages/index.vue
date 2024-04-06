<script setup>
const textButton = ref('Pokaż')
const showElement = ref(false)
const showSpan = (name) => {
  showElement.value = !showElement.value
  textButton.value = showElement.value ? 'Ukryj' : 'Pokaż'
  console.log('Komunikat w konsoli ' + name)
}
</script>

<template>
  <h1>Strona domowa</h1>
  <button @click="showSpan('Szymon')">{{ textButton }} coś</button>
  <br />
  <span v-if="showElement"> Pokazany element v-if :)</span>
  <br />
  <span v-show="showElement"> Pokazany element v-show :)</span>

  <ModalBasic
      :title="'Skasuj wszystkich'"
      v-if="showElement"
      @closeModal="showSpan('Janek')"
  />

</template>