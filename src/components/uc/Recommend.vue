<template>
    <div style="text:center">
        <p slot="header" style="text-align: center;">推广二维码</p>
        </br>
        <div class="show-qrcode" style="text-align: center;">
        <qriously :value="qvalue" :size="qsize" foreground="#fff" />
        </div>
        </br>
        <p slot="header" style="text-align: center;">推广链接：{{qvalue}}</p>
    </div>
</template>
<script>
import Vue from "vue";
import VueQriously from "vue-qriously";
Vue.use(VueQriously);

export default {
  components: {
    VueQriously
  },
  data() {
    return {
        qvalue: "",
        qsize: 200, 
    }
  },
  mounted:function() {
      this.getMember();
  },
 methods: {
    getMember() {
        //获取个人安全信息
        var self = this;
        this.$http
            .post(this.host + "/uc/approve/security/setting")
            .then(response => {
            var resp = response.body;
            
                this.user = resp.data;
                this.qvalue ="http://www.dogex.pro/#/register?recommend=" +this.user.username;
          
            });
        }
    }
}
</script>