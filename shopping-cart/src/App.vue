<template>
  <div class="App">
    <div v-for="item in items" :key="item.id">
      <!-- v-if="item.id % 2 === 0" -->
      <!--  v-bind:style="[
          item.id % 2
            ? { 'background-color': 'blue' }
            : { 'background-color': 'red' },
        ]" -->
      <Card
        v-bind:class="{ isOdd: item.id % 2 === 1 }"
        :name="item.name"
        :image="item.imageUrl"
      />
    </div>
    <!-- <h3>{{ text }}</h3>
    <input type="text" v-model="text" /> -->
  </div>
</template>

<script>
import Card from './Card';

export default {
  data: function () {
    return {
      text: 'hello world',
      items: [
        {
          id: 0,
          name: 'tiger',
          imageUrl: 'lion',
        },
        {
          id: 1,
          name: 'banana',
          imageUrl: 'strawberry',
        },
        {
          id: 2,
          name: 'computer',
          imageUrl: 'mouse',
        },
        {
          id: 3,
          name: 'babies',
          imageUrl: 'monkeys',
        },
      ],
    };
  },
  methods: {
    printHello: function () {
      console.log('hello');
    },
  },
  components: { Card },
  created: async function () {
    // You can directly change state like this:
    // this.items = [
    //   {
    //     id: 3,
    //     name: 'babies',
    //     imageUrl: 'monkeys',
    //   },
    // ];

    const fetchRobots = async (id, newItems) => {
      const res = await fetch(`https://robohash.org/${id}`);
      const newItem = {
        id,
        name: id,
        imageUrl: res.url,
      };
      newItems.push(newItem);
    };

    const newItems = [];
    const range = 1000;
    let id = Math.floor(Math.random() * range);

    let i = 0;
    const totalItems = 10;

    while (i < totalItems) {
      await fetchRobots(id, newItems);
      id = Math.floor(Math.random() * range);
      i += 1;
    }
    this.items = newItems;
  },
};
</script>
