<!-- src/components/LeftPanel.vue -->
<template>
  <div class="sidebar">
    <h2 class="sidebar-title">Folders</h2>
    <ul class="folder-list">
      <folder-node
        v-for="folder in folders"
        :key="folder.id"
        :folder="folder"
        @folderSelected="selectFolder"
      />
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import FolderNode from "./FolderNode.vue";

export default {
  components: { FolderNode },
  data() {
    return {
      folders: [],
    };
  },
  methods: {
    async loadFolders() {
      const response = await axios.get("http://127.0.0.1:8000/api/folders");
      this.folders = response.data;
    },
    selectFolder(folderId) {
      this.$emit("folderSelected", folderId);
    },
  },
  created() {
    this.loadFolders();
  },
};
</script>

<style scoped>
.sidebar {
  width: 250px;
  height: 100vh;
  background-color: #f4f4f4;
  padding: 20px;
  box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
  overflow-y: auto;
}

.sidebar-title {
  font-size: 1.5em;
  margin-bottom: 20px;
  color: #333;
}

.folder-list {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.folder-list li {
  padding: 10px 15px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.folder-list li:hover {
  background-color: #e0e0e0;
}
</style>
