<template>
  <div class="item">
    <span>{{ item.name }}</span>
  </div>
</template>

<script setup lang="ts">
interface Item {
  id: string;
  number: string;
}

const props = defineProps<{
  item: Item;
}>();
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
}

span {
  text-align: center;
}

</style>