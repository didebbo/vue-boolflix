<template>
  <ul class="tv">
    <li>
      {{ `ID: ${tv.id}` }}
    </li>
    <li>
      {{ `Title: ${tv.name}` }}
    </li>
    <li>
      {{ `Original Title: ${tv.original_name}` }}
    </li>
    <li>
      Language:
      <img
        :src="`https://flagcdn.com/16x12/${tv.original_language}.png`"
        :alt="tv.original_language"
      />
    </li>
    <li>
      {{ `Vote Average: ${tv.vote_average}` }}
    </li>
  </ul>
</template>

<script>
export default {
  name: "Tv",
  props: ["tv"],
};
</script>

<style>
</style>