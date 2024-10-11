<template>
  <div class="p-5">
    <h1 class="text-2xl mb-4">Демо компоненти</h1>

    <h2 class="text-xl mb-2">Кнопка</h2>
    <Button
      label="Натисни мене"
      color="blue"
      size="medium"
      @click="handleButtonClick"
    />

    <h2 class="text-xl mt-5 mb-2">Пошуковий випадаючий список</h2>
    <SearchableDropdown
      :items="items"
      :multiple="true"
      @update:selected="handleSelectionUpdate"
    />
  </div>
</template>

<script>
import Button from '../components/Button.vue';
import SearchableDropdown from '../components/SearchableDropdown.vue';

export default {
  components: {
    Button,
    SearchableDropdown
  },
  data() {
    return {
      items: ['Apple', 'Banana', 'Orange', 'Grapes', 'Strawberry'],
    };
  },
  methods: {
    handleButtonClick() {
      alert('Кнопка натиснута!');
    },
    handleSelectionUpdate(selectedItems) {
      console.log('Вибрані елементи:', selectedItems);
    }
  }
};
</script>

<style scoped>
</style>
