<template>
  <div class="main">
    <video playsinline></video>
    <button @click="paused ? continueStream() : takePhoto()">
      {{ paused ? 'Continue' : 'Take photo' }}
    </button>
    <canvas></canvas>
  </div>
</template>

<script>
export default {
  name: 'Main',
  data () {
    return {
      video: null,
      paused: false
    }
  },
  mounted() {
  //  const isSafari = !!navigator.userAgent.match(/Version\/[\d\.]+.*Safari/)
    this.startStream();
  },
  methods: {
    takePhoto() {
      this.video.pause();
      this.paused = true;

      const canvas = document.querySelector('canvas');
      const context = canvas.getContext('2d');

      canvas.width = this.video.videoWidth;
      canvas.height = this.video.videoHeight;

      context.drawImage(this.video, 0, 0, canvas.width, canvas.height);
      const imgSrc = canvas.toDataURL('image/png');

      window.location = 'image-receiver://' + imgSrc.slice(22);
    },
    startStream() {
      this.video = document.querySelector('video');

      var constraints = {
        audio: false,
        video: {
          facingMode: "user"
        }
      }

      navigator.mediaDevices.getUserMedia(constraints)
      .then(stream => {
        if ("srcObject" in this.video) {
          this.video.srcObject = stream;
        } else {
          this.video.src = window.URL.createObjectURL(stream);
        }

        this.video.play();
      })
      .catch(error => {
        console.log(error.name + ": " + error.message);
      })
    },
    continueStream() {
      this.video.play();
      this.paused = false;
    }
  }
}
</script>

<style scoped>
button {
  position: absolute;
  z-index: 2;
  top: 110vw;
  left: calc(50vw - 50px);
  width: 100px;
  height: 44px;
  border: solid 1px black;
  border-radius: 22px;
  background-color: white

}
video {
  position: relative;
  z-index: 1;
  width: 100vw;
  height: 133.3vw;
  background-color: #ccc;
}
canvas {
  display: none;
}

</style>
