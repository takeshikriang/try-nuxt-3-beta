<script>
export default {
  setup() {
    useMeta({
      script: [{ src: 'https://cdn.tailwindcss.com' }]
    });
  }
};
</script>

<template>
  <div class="container mx-auto">
    <StarWarsData />
  </div>
</template>
