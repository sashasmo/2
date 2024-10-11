<template>
  <div class="relative">
    <input
      type="text"
      placeholder="Search..."
      v-model="searchTerm"
      @focus="isOpen = true"
      @blur="closeDropdown"
      class="border rounded px-3 py-2 w-full"
    />
    <div
      v-if="isOpen"
      class="absolute z-10 w-full bg-white border rounded mt-1"
      @mouseover="isMouseOver = true"
      @mouseleave="isMouseOver = false"
    >
      <ul class="max-h-60 overflow-y-auto">
        <li
          v-for="(item, index) in filteredItems"
          :key="index"
          @click="selectItem(item)"
          class="px-3 py-2 hover:bg-gray-200 cursor-pointer"
        >
          {{ item }}
        </li>
        <li v-if="filteredItems.length === 0" class="px-3 py-2 text-gray-500">
          Нічого не знайдено
        </li>
      </ul>
      <button @click="clearSelection" class="px-3 py-2 text-red-500">Очистити</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
      required: true,
    },
    multiple: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      searchTerm: '',
      selectedItems: [],
      isOpen: false,
      isMouseOver: false,
    };
  },
  computed: {
    filteredItems() {
      return this.items.filter(item => 
        item.toLowerCase().includes(this.searchTerm.toLowerCase())
      );
    }
  },
  methods: {
    selectItem(item) {
      if (this.multiple) {
        if (this.selectedItems.includes(item)) {
          this.selectedItems = this.selectedItems.filter(i => i !== item);
        } else {
          this.selectedItems.push(item);
        }
      } else {
        this.selectedItems = [item];
        this.isOpen = false;
      }
      this.$emit('update:selected', this.selectedItems);
    },
    clearSelection() {
      this.selectedItems = [];
      this.$emit('update:selected', this.selectedItems);
    },
    closeDropdown() {
      if (!this.isMouseOver) {
        this.isOpen = false;
      }
    }
  }
};
</script>

<style scoped>
input:focus {
  outline: none;
  border-color: #4A90E2;
}
</style>
