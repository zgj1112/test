<template>
  <h1>{{ msg }}</h1>
  <input @change="testfun" type="file" />
  <a-upload
    name="file"
    action="https://www.mocky.io/v2/5cc8019d300000980a055e76"
    :headers="headers"
    @change="handleChange"
  >
    <a-button> Click to Upload </a-button>
  </a-upload>
</template>
<script setup lang="ts">
import { ref } from "vue";
import { message } from "ant-design-vue";
import { UploadOutlined } from "@ant-design/icons-vue";
import type { UploadChangeParam } from "ant-design-vue";

defineProps<{ msg: string }>();
let headers = {
  authorization: "authorization-text",
};
const handleChange = (info: any) => {
  if (info.file.status !== "uploading") {
    const files = info.fileList;
    if (files.length > 0) {
      const file = files[0].originFileObj; // 当前操作的文件对象
      const reader = new FileReader();
      // text类型
      reader.readAsText(file, "utf-8");
      reader.onload = function () {
        console.log(this.result); // 文件内容
      };
    }
  }
};
// const handleChange = (e: any) => {
//   console.log(e);
//   const files = e.fileList[0];
//   if (files.length > 0) {
//     const file = files[0]; // 当前操作的文件对象
//     const reader = new FileReader();
//     if (/text+/.test(file.type)) {
//       // text类型
//       reader.readAsText(file, "utf-8");
//     } else if (/image+/.test(file.type)) {
//       // image类型
//       reader.readAsDataURL(file);
//     }
//     reader.onload = function () {
//       console.log(this.result); // 文件内容
//     };
//   }
// };
const testfun = (e: any) => {
  const files = e.target.files;
  console.log(files);

  if (files.length > 0) {
    const file = files[0]; // 当前操作的文件对象
    const reader = new FileReader();
    if (/text+/.test(file.type)) {
      // text类型
      reader.readAsText(file, "utf-8");
    } else if (/image+/.test(file.type)) {
      // image类型
      reader.readAsDataURL(file);
    }
    reader.onload = function () {
      console.log(this.result); // 文件内容
    };
  }
};
</script>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
