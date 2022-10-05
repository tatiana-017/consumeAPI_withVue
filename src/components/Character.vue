<template>
  <tr>
    <td>{{ character.name }}</td>
    <td>{{ character.status }}</td>
    <td>{{ character.species }}</td>
    <td>{{ character.gender }}</td>
  </tr>
</template>

<script>
export default {
  props: ["character"],
};
</script>