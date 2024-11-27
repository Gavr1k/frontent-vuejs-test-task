<template>
  <div class="item" @click="handleClick">
    <span>{{ item.name }}</span>
  </div>
</template>

<script setup lang="ts">
import { defineProps, defineEmits } from 'vue';

interface Item {
  id: number;
  name: string;
}

const props = defineProps<{ item: Item }>();
const emit = defineEmits<{
  (e: 'select', item: Item): void;
}>();

const handleClick = () => {
  emit('select', props.item);
};
</script>

<style scoped>
.item {
  width: 100%;
  height: 40px;
  border: 1px solid black;
  border-radius: 20px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

span {
  text-align: center;
}
</style>
