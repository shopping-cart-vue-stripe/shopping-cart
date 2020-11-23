<template>
  <div class="card-component">
    <h3>{{ name }}</h3>
    <div><img :src="image" alt="Robot" /></div>
    <button>Add To Cart</button>
  </div>
</template>

<script>
export default {
  props: ['name', 'image'],
};
</script>

<style>
.card-component {
  border: 3px solid blue;
  text-align: center;
  background-color: rebeccapurple;
}
.isOdd {
  background-color: blue;
}
</style>
