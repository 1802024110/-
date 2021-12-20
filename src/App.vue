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
      >下载</v-btn>
    </div>
  </v-app>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      text: "",
      downloadUrl: '',
    }
  },
  watch: {
    text(val) {
      if(val==''){
        this.downloadUrl = ''
        return ''
      }
      // 正则表达式
      let reg = /id=(\d+)&/;
      let url = this.text;
      let id = url.match(reg)[1];
      this.downloadUrl = id
      axios.get(`http://bbq.bilibili.com/bbq/app-bbq/sv/detail?svid=${id}&version=1.3.0&platform=h5`).then(res => {
        console.log(res.data);
      })
    }
  },
/*   computed: {
    downloadUrl() {
      if(this.text==''){
        return ''
      }
      // 正则表达式
      let reg = /id=(\d+)&/;
      let url = this.text;
      let id = url.match(reg)[1];
      // // axiso访问
      // axios.get(`https://bbq.bilibili.com/bbq/app-bbq/sv/detail?svid=${id}&version=1.3.0&platform=h5`).then(res => {
      //   console.log(res.data);
      // })
      return id;
    }
  }, */
};
</script>
