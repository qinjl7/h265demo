<template>
  <div class="dashboard-container">
    <div class="dashboard-text">name: h265demo</div>
    <video
      id="player"
      height="360"
      width="200"
      class="video-js vjs-big-play-centered"
      controls
      autoplay
      loop
      ish265
      islive
      hasvideo
      hasaudio
    >
      <source
        src="https://livevideo-test.slivee.com/slivee-test/2sB_nV6-F6J_h265test.flv"
        type="video/x-flv"
      />
    </video>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import videojs from "video.js";
import "./plugin";

export default {
  name: "Dashboard",
  computed: {
    ...mapGetters(["name"]),
  },
  mounted() {
    let player = videojs("player", {
      techOrder: ["html5", "flvh265"],
      controlBar: {
        volumePanel: { inline: false },
        pictureInPictureToggle: false,
      },
    });
    player.on("error", function () {
      console.log(this.error());
    });
    player.on("loadstart", function () {
      console.log("loadstart");
      console.time();
    });
    player.on("loadedmetadata", function () {
      console.log("loadedmetadata");
      console.timeEnd();
    });
  },
};
</script>

<style lang="scss" scoped>
.dashboard {
  &-container {
    margin: 30px;
  }
  &-text {
    font-size: 30px;
    line-height: 46px;
  }
}
</style>
