<!-- src/components/FolderNode.vue -->
<template>
  <li type="none">
    <span @click="select"> 📁 {{ folder.name }}</span>
    <ul type="none" v-if="folder.children && folder.children.length">
      <folder-node
        v-for="child in folder.children"
        :key="child.id"
        :folder="child"
        @folderSelected="$emit('folderSelected', $event)"
      />
    </ul>
  </li>
</template>

<script>
export default {
  props: {
    folder: Object,
  },
  methods: {
    select() {
      this.$emit("folderSelected", this.folder.id);
    },
  },
};
</script>
