<template>
  <h1>Packrat!</h1>
  <form @submit.prevent="addNewItem">
    <label>New item</label>
    <input v-model="newItem" name="newItem">
    <button>Add item</button>
  </form>
  <ul>
    <li v-for="(item, index) in items" :key="item.id" class="listItem">
      <h3 :class="{packed: item.packed}" @click="togglePacked(item)">
        {{ item.name }}
      </h3>
      <button @click="removeItem(index)">Remove</button>
    </li>
  </ul>
</template>

<script>
import { ref, VueElement } from 'vue';

export default{
  setup(){
    const newItem = ref('');
    const items = ref([]);

    function addNewItem(){
      items.value.push({ 
        id: Date.now(),
        packed: false, 
        name: newItem.value 
      });

      newItem.value = '';
    }

    function togglePacked(item){
      item.packed = !item.packed;
    }

    function removeItem(index){
      items.value.splice(index, 1);
    }

    return{
      items,
      newItem,
      addNewItem,
      togglePacked,
      removeItem,
    }
  }
}

</script>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}

.packed {
  text-decoration: line-through;
}

.listItem{
  cursor: pointer;
}
</style>
