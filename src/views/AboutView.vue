  <!-- 6c. v-if on Template -->
<template v-if="ok">
  <!-- 6a. v-for with a object -->
 <div>
    <h3>v-for with an Object</h3>
    <ul>
      <li v-for="(value, key) in user" :key="key">
        {{ key }}: {{ value }}
      </li>
    </ul>
  </div>
  <!-- 6b. v-for with a Range -->
  <div>
    <h3>v-for with a Range</h3>
    <ul>
      <li v-for="number in numberRange" :key="number">
        Item {{ number }}
      </li>
    </ul>
  </div>
   <!-- 6d. v-for with v-if -->
   <div>
    <h3>v-for with v-if</h3>
    <ul>
      <li v-for="item in filteredItems" :key="item.id">
        {{ item.name }}
      </li>
    </ul>
  </div>
</template>
  <script>
export default {
  data() {
    return {
      user: {
        name: 'John Doe',
        age: 30,
        email: 'john@example.com',
      },
      items: [
        { id: 1, name: 'Item 1', condition: true },
        { id: 2, name: 'Item 2', condition: false },
        { id: 3, name: 'Item 3', condition: true },
      ],
    };
  },
  computed: {
    numberRange() {
      return Array.from({ length: 5 }, (_, index) => index + 1);
    },
    filteredItems() {
      return this.items.filter((item) => item.condition);
    },
  },
};

  </script>

