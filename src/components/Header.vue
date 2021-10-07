<template>
  <header>
    <div class="fluid-container">
      <div class="logo">
        <a href="#"
          ><img
            src="https://fontmeme.com/permalink/211007/bc001285b4acd0b4828e3939d958e947.png"
            alt="netflix-font"
            border="0"
        /></a>
      </div>
      <form>
        <div class="query">
          <input type="text" v-model="query" />
        </div>
        <div class="submit">
          <button @click.prevent="$emit('getQuery', query)">Search</button>
        </div>
      </form>
    </div>
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
  padding: 1em;

  .fluid-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    .logo {
      color: red;
      font-size: 0.8em;
      img {
        height: 2.5em;
      }
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
}
</style>