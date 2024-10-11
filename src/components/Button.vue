<template>
  <button
    :class="buttonClass"
    @click="handleClick"
  >
    <span v-if="icon" class="mr-2">
      <i :class="icon"></i>
    </span>
    {{ label }}
  </button>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      required: true
    },
    color: {
      type: String,
      default: 'blue'
    },
    size: {
      type: String,
      default: 'medium'
    },
    icon: {
      type: String,
      default: null
    }
  },
  computed: {
    buttonClass() {
      const colorClasses = {
        red: 'bg-red-500 text-white',
        blue: 'bg-blue-500 text-white',
        green: 'bg-green-500 text-white',
      };
      const sizeClasses = {
        small: 'py-1 px-2 text-sm',
        medium: 'py-2 px-4',
        large: 'py-3 px-6 text-lg',
      };
      return `${colorClasses[this.color]} ${sizeClasses[this.size]} rounded focus:outline-none`;
    }
  },
  methods: {
    handleClick() {
      this.$emit('click');
    }
  }
};
</script>

<style scoped>
button {
  transition: background-color 0.3s ease;
}
button:hover {
  opacity: 0.9;
}
</style>
