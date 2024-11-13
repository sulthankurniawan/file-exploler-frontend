<!-- src/components/RightPanel.vue -->
<template>
  <div class="right-panel">
    <h3>Subfolders:</h3>
    <div class="folder-cards">
      <div
        class="folder-card"
        v-for="subfolder in subfolders"
        :key="subfolder.id"
        @click="selectSubfolder(subfolder.id)"
      >
        <i class="fa fa-folder folder-icon" aria-hidden="true"></i>
        <div class="folder-name">{{ subfolder.name }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: {
    folderId: Number,
  },
  data() {
    return {
      subfolders: [],
    };
  },
  watch: {
    folderId: "loadSubfolders",
  },
  methods: {
    async loadSubfolders() {
      if (this.folderId) {
        const response = await axios.get(
          `http://127.0.0.1:8000/api/folders/${this.folderId}`
        );
        this.subfolders = response.data;
      } else {
        this.subfolders = [];
      }
    },
    selectSubfolder(subfolderId) {
      console.log("Selected subfolder:", subfolderId);
    },
  },
};
</script>

<style scoped>
.right-panel {
  padding: 10px;
}

.folder-cards {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.folder-card {
  background-color: #ffffff;
  border: 1px solid #ddd;
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  padding: 15px;
  width: 150px;
  text-align: center;
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
}

.folder-card:hover {
  transform: scale(1.05);
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
}

.folder-icon {
  font-size: 24px;
  margin-bottom: 10px;
}

.folder-name {
  font-weight: bold;
}
</style>
