<template>
  <ul>
    <resource-item
      v-for="{ id, title, description, link } in resources"
      :key="id"
      :id="id"
      :title="title"
      :description="description"
      :link="link"
    />
  </ul>
</template>

<script>
import ResourceItem from '@/components/learning-resources/ResourceItem';

export default {
  components: {
    ResourceItem
  },
  inject: ['resources'],
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: auto;
  padding: 0;
  max-width: 40rem;
}
</style>
