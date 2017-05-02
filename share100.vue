<template>
<div class="content" style="background:#ffffff;">
  <div class="nonole" style="position:relative;">
    <img class="share100-backImg" src="http://download.dl.quzhuan.me/image/redpack/img/share100-bg.png" alt="">
    <div class="share100-guize">活动规则</div>
    <div class="share100-con">
      <p style="color:#333;">1、您的好友点击接受您的邀请，下载红包多app病使用被邀请的微信登录。</p>
      <p style="color:#333;">2、您的好友打开红包多app接受您的好友邀请，且您是您的好友红包多app好友列表中的第一个好友。</p>
      <p style="color:#999">温馨提示：您的好友登红包多app前，没有点过其他人分享的微信卡片，您和您的好友不可以是同一部手机。</p>
      <p style="color:#333;">3、邀请成功后，多多会发随机提现锦囊奖励，最高100元。</p>
    </div>
    <div class="share100-footer" @click="getShare">
      <img src="http://download.dl.quzhuan.me/image/redpack/img/share100-anniu.png" alt="">
    </div>
  </div>
</div>
</template>
<script>
import $ from 'zepto';
export default {
  data() {
    return {};
  },
  methods: {
    setupWebViewJavascriptBridge: function(callback) {
      if (window.WebViewJavascriptBridge) {
        return callback(window.WebViewJavascriptBridge);
      };
      var WVJBIframe = document.createElement('iframe');
      WVJBIframe.style.display = 'none';
      WVJBIframe.src = 'wvjbscheme://__BRIDGE_LOADED__';
      document.documentElement.appendChild(WVJBIframe);
      setTimeout(function() {
        document.documentElement.removeChild(WVJBIframe);
      }, 0);
    },
    getShare: function() {
      var ua = navigator.userAgent.toLowerCase();
      var isAndroid = /android/.test(ua);
      var isiOS = /iphone|ipad|ipod/.test(ua);
      if (isiOS) {
        this.setupWebViewJavascriptBridge(function(bridge) {
          bridge.callHandler('iOSredPacketShare', {
            activityNumber: '01'
          }, function(response) {});
        });
      };
      if (isAndroid) {
        window.WebViewJavascriptBridge.callHandler('submitFromWeb', {
          'code': '1000',
          'activityNumber': '01'
        }, function(responseData) {});
      };
    }
  },
  ready() {
    $('title').text('好友邀请');
  }
};
</script>
<style>
.share100-backImg {
  width: 100%;
}

.share100-guize {
  width: 164px;
  height: 36px;
  background: url('http://download.dl.quzhuan.me/image/redpack/img/share100-guizebg.png') no-repeat;
  background-size: 100%;
  color: #fff;
  text-align: center;
  line-height: 36px;
  font-size: 20px;
  position: absolute;
  top: 31%;
  left: 50%;
  margin-left: -82px;
}

.share100-con {
  position: absolute;
  top: 40%;
  width: 80%;
  margin-left: 12%;
}

.share100-con p {
  margin-top: 10px;
}

.share100-footer {
  width: 50%;
  position: absolute;
  bottom: 0;
  left: 25%;
}

.share100-footer img {
  width: 100%;
}
</style>
