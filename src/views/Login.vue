<template>
  <div class="login-homepage-hero-module">
    <div class="login-video-container">
      <div :style="fixStyle" class="login-filter">
        <LoginForm></LoginForm>
      </div>
      <video :style="fixStyle" autoplay loop muted class="login-fillWidth"
             v-on:canplay="canplay">
        <source src="../assets/video/bgVideo3.mp4" type="video/mp4"/>
      </video>
      <!-- <div class="login-poster login-hidden" v-if="!videoCanPlay">
        <img :style="fixStyle" src="../assets/container_bg.jpg" alt="视频封面">
      </div> -->
    </div>
  </div>
</template>
<script>
import LoginForm from "@/views/LoginForm.vue";

export default {
  name: "Login",
  components: {
    LoginForm
  },
  data() {
    return {
      videoCanPlay: false,
      fixStyle: ''
    }
  },
  methods: {
    canplay() {
      this.videoCanPlay = true
    }
  },
  mounted: function () {
    //主要是检测窗口缩放视频也同步大小
    window.onresize = () => {
      const windowWidth = document.body.clientWidth
      const windowHeight = document.body.clientHeight
      const windowAspectRatio = windowHeight / windowWidth
      let videoWidth
      let videoHeight
      if (windowAspectRatio < 0.5625) {
        videoWidth = windowWidth
        videoHeight = videoWidth * 0.5625
        this.fixStyle = {
          height: windowWidth * 0.5625 + 'px',
          width: windowWidth + 'px',
          'margin-bottom': (windowHeight - videoHeight) / 2 + 'px',
          'margin-left': 'initial'
        }
      } else {
        videoHeight = windowHeight
        videoWidth = videoHeight / 0.5625
        this.fixStyle = {
          height: windowHeight + 'px',
          width: windowHeight / 0.5625 + 'px',
          'margin-left': (windowWidth - videoWidth) / 2 + 'px',
          'margin-bottom': 'initial'
        }
      }
    }
    window.onresize();
  }
}
</script>

<style scoped>
.login-homepage-hero-module,
.login-video-container {
  position: relative;
  height: 100vh;
  overflow: hidden;
}

.login-video-container .login-poster img,
.login-video-container video {
  z-index: 0;
  position: absolute;
}

.login-video-container .login-filter {
  z-index: 1;
  position: absolute;
}
</style>