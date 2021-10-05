<template>
  <header>
    <form>
      <input type="text" v-model="query" />
      <button @click.prevent="$emit('getQuery', query)">Search</button>
    </form>
  </header>
</template>

<script>
export default {
  name: "Header",
  data() {
    return {
      query: "",
    };
  },
};
</script>

<style>
</style>