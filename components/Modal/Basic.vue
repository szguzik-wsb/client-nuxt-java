<script setup>
const props = defineProps({
  title: {
    type: String,
    default: () => 'Domyślna wartość'
  },
  likes: Number
})

const newTitle = ref(props.title)

const emit = defineEmits(['closeModal']);
const closeModal = () => emit('closeModal');
const changeTitele = () => newTitle.value = 'Nowy tytul'

</script>

<template>
  <div class="modal">

    <div class="content">
      <h1>Modal</h1>
      <span>{{ newTitle }}</span>
      <br>
      <button>Skasuj wszystkich</button>
      <button @click="changeTitele">Zmien tytul</button>
      <button @click="closeModal">Close</button>
    </div>

  </div>
</template>

<style scoped lang="scss">
.modal {
  display: block;
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  color: #333;
  padding: 10px;
  margin-bottom: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;

  h1 {
    font-size: 1.5em;
    margin-bottom: 5px;
  }

  p {
    font-size: 1.2em;
  }

  .content {
    background-color: #fff;
    padding: 20px;
    border-radius: 5px;
    width: 50%;
    margin: 10% auto 0;
  }
}
</style>