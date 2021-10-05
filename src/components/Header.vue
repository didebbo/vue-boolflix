<template>
  <header>
    <div class="logo">
      <h1>Boolflix</h1>
    </div>
    <form>
      <div>
        <input type="text" v-model="query" />
      </div>
      <div>
        <button @click.prevent="$emit('getQuery', query)">Search</button>
      </div>
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

<style scoped lang="scss">
header {
  background-color: black;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1em;

  .logo {
    color: red;
    font-size: 0.8em;
  }

  form {
    display: flex;
    align-items: center;
    > * {
      padding: 0 0.5em;

      > * {
        padding: 0.2em;
        font-size: 0.9em;
      }
    }
  }
}
</style>