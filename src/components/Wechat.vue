<template>
  <div>
    <el-button type="primary" @click="getQrcode">加载二维码</el-button>
    <template v-show="isShowQrcode">
      <img id="qrcode" :src="qrcodeImg" />
    </template>
    <el-button type="primary" @click="doLogin">登陆</el-button>
  </div>
</template>

<script>
export default {
  name: "Wechat",
  props: {},
  data() {
    return {
      qrcodeImg: "",
      qrcodeResponse: null,
      isShowQrcode: false
    };
  },
  methods: {
    doLogin() {
      const that = this;
      that
        .axios({
          url: "/api/checkLogin/" + that.qrcodeResponse.uuid,
          method: "get"
        })
        .then(response => {
          if (response.data.status == 200) {
            alert("成功！");
          }
        })
        .catch(error => {
          console.log(error);
        });
    },
    getQrcode() {
      const that = this;
      that
        .axios({
          url: "/api/wxQrcode",
          method: "get"
        })
        .then(response => {
          console.log(response);
          that.qrcodeResponse = response.data.data;
          return "data:image/png;base64," + that.qrcodeResponse.qrcode;
        })
        .then(data => {
          this.qrcodeImg = data;
        })
        .catch(error => {
          console.log(error);
        });
      return this.qrcodeImg;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus"></style>
