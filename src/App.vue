<template>
  <v-app>
    <div  style="width:300px;margin:50% auto">
    <v-text-field
    class="rounded-pill"
          solo
          hide-details='auto'
          label="请输入分享链接"
          v-model="text"
    ></v-text-field>
    <!-- 链接显示 -->
    <v-textarea
    class="pt-4"
          outlined
          readonly
          name="input-7-4"
          label="下载链接"
          :value='downloadUrl'
        ></v-textarea>
  <!-- 下载视频 -->
    <v-btn
      class="rounded-pill"
      color="primary"
      @click="download"
      >下载</v-btn>
    </div>
  </v-app>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      text: "#轻视频# https://bbq.bilibili.com/video/?id=1635755626020555348&shu=gn871",
    }
  },
  computed: {
    downloadUrl() {
      // 正则表达式
      let reg = /https:\/\/bbq.bilibili.com\/video\/\?id=(\d+)&shu=gn871/;
      let url = this.text;
      let id = url.match(reg)[1];
      // axiso访问
      axios.get(`https://bbq.bilibili.com/bbq/app-bbq/sv/detail?svid=${id}&version=1.3.0&platform=h5`).then(res => {
        console.log(res.data);
      })
      return id;
    }
  },
};
</script>
