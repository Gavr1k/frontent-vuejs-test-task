<template>
  <section class="header-section">
    <div class="header-section__wrapper">
      <div class="block">
        <template v-for="userItem in userSelectedItems" :key="userItem.id">
          <itemUI class="user-items__item" :item="userItem"></itemUI>
        </template>
        <span>Selected: {{userSelectedItems.length}}/6</span>
      </div>
      <div class="block">
          <template v-if="Object.keys(itemSelected).length">
            <itemUI class="user-items__item" :item="itemSelected"></itemUI>
          </template>
          <template v-else>
            <span>Selected item</span>
          </template>
      </div>
    </div>
  </section>
  <section class="items-section">
    <div class="user-items">
      <template v-for="userItem in userItems" :key="userItem.id">
        <itemUI @click="handleSelectUserItem(userItem)" class="user-items__item" :item="userItem"></itemUI>
      </template>
    </div>
    <div class="selected-items">
      <template v-for="item in items" :key="item.id">
        <itemUI @click="handleSelectItem(item)" class="user-items__item" :item="item"></itemUI>
      </template>
    </div>
  </section>
</template>

<script setup lang="ts">
import itemUI from './components/itemUi.vue';
import userItemsMock from './mock-data/userItems';
import itemsMock from './mock-data/items';
import {ref} from 'vue';

const userItems = ref(userItemsMock);
const items = ref(itemsMock);

const userSelectedItems = ref([]);
const itemSelected = ref({});

const handleSelectUserItem = (item) => {
  if (userSelectedItems.value.length === 6) return;
  userSelectedItems.value.push(item);
};

const handleSelectItem = (item) => {
  itemSelected.value = item;
}

</script>
<style scoped>

.body {
  box-sizing: border-box;
}

.header-section {
  margin-bottom: 20px;
}

.header-section__wrapper {
  display: flex;
  justify-content: space-between;
}

.block {
  width: 20%;
  min-height: 30px;
  border: 1px solid black;
}

.items-section {
  display: flex;
  justify-content: space-between;
}

.user-items, .selected-items {
  border: 1px solid black;
  border-radius: 10px;
  width: 40%;
  display: flex;
  flex-wrap: wrap;
}

.user-items__item {
  width: 30%;
  margin: 1rem;
}

</style>
