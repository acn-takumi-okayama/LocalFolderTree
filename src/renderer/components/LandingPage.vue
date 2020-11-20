<template>
  <div id="wrapper">
    <main>
      <!-- system-information></system-information -->
      <div>
        <h3>
          選択したフォルダ配下のフォルダ名とファイル名をエクセルに出力します
        </h3>
        <el-button icon="el-icon-search" circle　@click="selectDir"></el-button>
        <p>{{ dirPath }}</p>
        <el-button type="primary" @click="dispDir">表示</el-button>
        <el-button type="success">出力</el-button>
        <div>
          {{ this.dirList }}
        </div>
      </div>
    </main>
  </div>
</template>

<script>
//import SystemInformation from './LandingPage/SystemInformation'
import { remote } from "electron";
import * as fs from "fs";
export default {
  name: "landing-page",
  //components: { SystemInformation },
  data() {
    return {
      dirPath: "フォルダを選択してください。",
      dirList: null,
    };
  },
  methods: {
    selectDir: function () {
      this.dirPath = remote.dialog.showOpenDialog(null, {
        properties: ["openDirectory"],
        title: "Select a Folder",
        defaultPath: ".",
      })[0];
      console.log(this.dirPath);
    },
    dispDir: function () {
      const dirents = fs.readdirSync(dir, { withFileTypes: true });
      const dirs = [];
      for (const dirent of dirents) {
        if (dirent.isDirectory()) dirs.push(`${dir}/${dirent.name}`);
        if (dirent.isFile()) files.push(`${dir}/${dirent.name}`);
      }
      for (const d of dirs) {
        files = readdirRecursively(d, files);
      }
      return files;
    },
  },
};
</script>

<style scoped>
</style>
