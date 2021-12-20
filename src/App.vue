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
    <a :href="downloadUrl">
      <v-btn
      v-if="downloadUrl"
      class="rounded-pill"
      color="primary"
      >下载</v-btn>
    </a>
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
  methods: {
    // 点击下载事件

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
      axios.get(`https://api.nodream.ml/api/qsp?id=${id}`).then(res => {
        // 返回的status如果是200，则说明请求成功
        if (res.status === 200) {
          this.downloadUrl = res.data.data.data.play.url
        }
      }).catch(err => {
        // 请求失败,再次请求
        axios.get(`https://api.nodream.ml/api/qsp?id=${id}`).then(res => {
        // 返回的status如果是200，则说明请求成功
        if (res.status === 200) {
          this.downloadUrl = res.data.data.data.play.url
        }
      })
        console.log(err);
      })
    }
  }
};
</script>
