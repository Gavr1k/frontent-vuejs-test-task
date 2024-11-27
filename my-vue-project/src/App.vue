<template>
  <section class="header-section">
    <div class="header-section__wrapper">
      <div class="block">
        <template v-for="userItem in userSelectedItems" :key="userItem.id">
          <ItemUI
            class="user-items__item"
            :item="userItem"
            @select="handleDeselectUserItem"
          />
        </template>
        <span>Selected: {{ userSelectedItems.length }}/6</span>
      </div>
      <div class="block">
        <template v-if="itemSelected">
          <ItemUI
            class="user-items__item"
            :item="itemSelected"
            @select="handleDeselectItem"
          />
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
        <ItemUI
          @select="handleSelectUserItem"
          class="user-items__item"
          :item="userItem"
        />
      </template>
    </div>
    <div class="selected-items">
      <template v-for="item in items" :key="item.id">
        <ItemUI
          @select="handleSelectItem"
          class="user-items__item"
          :item="item"
        />
      </template>
    </div>
  </section>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import ItemUI from './components/ItemUI.vue';
import userItemsMock from './mock-data/userItems';
import itemsMock from './mock-data/items';

interface Item {
  id: number;
  name: string;
}

const userItems = ref<Item[]>(userItemsMock);
const items = ref<Item[]>(itemsMock);

const userSelectedItems = ref<Item[]>([]);
const itemSelected = ref<Item | null>(null);

const handleSelectUserItem = (item: Item) => {
  if (userSelectedItems.value.length < 6 && !userSelectedItems.value.includes(item)) {
    userSelectedItems.value.push(item);
  }
};

const handleDeselectUserItem = (item: Item) => {
  userSelectedItems.value = userSelectedItems.value.filter(
    (i) => i.id !== item.id
  );
};

const handleSelectItem = (item: Item) => {
  itemSelected.value = item;
};

const handleDeselectItem = () => {
  itemSelected.value = null;
};
</script>

<style scoped>
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

.user-items,
.selected-items {
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
