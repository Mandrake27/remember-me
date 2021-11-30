<template>
  <base-card>
    <base-button
      type="button"
      :mode="storedResButtonMode"
      @click="setSelectedTab('stored-resources')"
    >Stored Resources
    </base-button>
    <base-button
      type="button"
      :mode="addResButtonMode"
      @click="setSelectedTab('add-resource')"
    >Add Resource
    </base-button>
  </base-card>
  <keep-alive>
    <component :is="selectedTab" />
  </keep-alive>
</template>

<script>
import StoredResources from '@/components/learning-resources/StoredResources.vue';
import AddResource from '@/components/learning-resources/AddResource.vue';

export default {
  components: {
    StoredResources,
    AddResource
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation.',
          link: 'https://vuejs.org'
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google...',
          link: 'https://google.com'
        }
      ]
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    }
  },
  provide() {
    return {
      resources: this.storedResources,
      addItem: this.addResource,
      deleteItem: this.deleteItem
    };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResource(newResource) {
      const id = newResource.title.toLowerCase().split(' ').join('-');
      this.storedResources.unshift({
        id,
        ...newResource
      });
      this.selectedTab = 'stored-resources';
    },
    deleteItem(id) {
      const resIndex = this.storedResources.findIndex(res => res.id === id);
      this.storedResources.splice(resIndex, 1);
    }
  }
};
</script>
