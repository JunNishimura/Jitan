<template>
  <div class="home">
    <div class="video-wrapper">
      <youtube :resize="true" video-id="MkUIPxeuasM" ref="video1" />
      <youtube :resize="true" video-id="zULDpf44BJE" ref="video2" />
      <youtube :resize="true" video-id="AEJeq5ut_GQ" ref="video3" />
      <youtube :resize="true" video-id="VwEKWcyG3rU" ref="video4" />
      <video src="@/assets/video/hannya.mp4" controls id="hannya-video" ref="hannyaVideo" />
      <youtube :resize="true" video-id="kJ0L_WzI9QU" ref="video5" />
      <youtube :resize="true" video-id="2Lmr6mX7sOM" ref="video6" />
      <youtube :resize="true" video-id="2CDq8uSpass" ref="video7" />
      <youtube :resize="true" video-id="0Tq2gIUwHdA" ref="video8" />
      <div v-if="!isPlaying" @click="startVideo" class="masking-center">
        <div class="image-wrapper">
          <img src="@/assets/images/play.png">
        </div>
      </div>
      <div v-if="!isPlaying" class="masking-all" />
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import VueYoutbe from 'vue-youtube'
Vue.use(VueYoutbe)

export default {
  data() {
    return {
      isPlaying: false,
    }
  },
  methods: {
    ready() {
      console.log("ready")
    },
    playing() {
      console.log("playing")
      this.isPlaying = true
    },
    paused() {
      console.log("paused")
      this.isPlaying = false
    },
    ended() {
      console.log("ended")
      this.isPlaying = false
    },
    startVideo() {
      const windowWidth = window.innerWidth
      const windowHeight = window.innerHeight
      const refArray = [this.$refs.video1, this.$refs.video2, this.$refs.video3, this.$refs.video4, this.$refs.video5, this.$refs.video6, this.$refs.video7, this.$refs.video8]

      const hannyaVideo = document.getElementById("hannya-video")
      hannyaVideo.playbackRate = 8
      hannyaVideo.width = windowWidth / 3
      hannyaVideo.height = windowHeight / 3
      hannyaVideo.play()

      refArray.forEach(video => {
        // video.player.mute()
        video.player.setVolume(3)
        video.player.playVideo()
      })

      this.isPlaying = true;
    }
  },
  mounted() {
    const windowWidth = window.innerWidth
    const windowHeight = window.innerHeight
    const refArray = [this.$refs.video1, this.$refs.video2, this.$refs.video3, this.$refs.video4, this.$refs.video5, this.$refs.video6, this.$refs.video7, this.$refs.video8]

    // iframeの映像設定
    refArray.forEach(video => {
      video.width = windowWidth / 3
      video.height = windowHeight / 3
      video.player.setPlaybackRate(2)
    })
    
    // 般若心経の映像設定
    const hannyaVideo = document.getElementById("hannya-video")
    hannyaVideo.playbackRate = 8
    hannyaVideo.width = windowWidth / 3
    hannyaVideo.height = windowHeight / 3
  },
  beforeDestroy() {
    this.isPlaying = false
  }
};
</script>

<style scoped lang="scss">
.home {
  width: 100vw;
  height: 100vh;
  background-color: #000;
  overflow: hidden;
}
.video-wrapper {
  display: flex;
  flex-wrap: wrap;
}
.masking-center {
  background-color: #000f;
  opacity: 1;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  height: 33%;
  width: 33%;
  z-index: 2;
}
.masking-all {
  background-color: #000;
  opacity: 1;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  height: 100vh;
  width: 100vw;
  z-index: 1;
}
.image-wrapper {
  width: 100%;
  height: 100%;
  position: relative;
}
.image-wrapper img {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  cursor: pointer;
}
</style>
