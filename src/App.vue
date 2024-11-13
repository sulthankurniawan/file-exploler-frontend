<!-- src/App.vue -->
<template>
  <div id="app" class="explorer">
    <div class="left-panel">
      <left-panel @folderSelected="selectFolder" />
    </div>
    <div class="right-panel">
      <right-panel :folderId="selectedFolderId" />
    </div>
  </div>
</template>

<script>
import LeftPanel from "./components/LeftPanel.vue";
import RightPanel from "./components/RightPanel.vue";

export default {
  components: { LeftPanel, RightPanel },
  data() {
    return {
      selectedFolderId: null,
    };
  },
  methods: {
    selectFolder(folderId) {
      this.selectedFolderId = folderId;
    },
  },
};
</script>

<style>
.explorer {
  display: flex;
}

.left-panel,
.right-panel {
  width: 50%;
  padding: 10px;
}
</style>
