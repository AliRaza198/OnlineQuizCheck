<template>
  <div class="camera">
    <div class="inner_section">
      <h2>Camera Component</h2>
      <div v-if="!cameraOn">
        <video ref="videoRef" :src="videoSrc" autoplay></video>
        <div>
          <button @click="startRecording" :disabled="isRecording">Start Recording</button>
          <button @click="stopRecording" :disabled="!isRecording">Stop Recording</button>
          <button @click="saveRecording" :disabled="!isRecording || !videoUrl">Save Recording</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name:'CameraRecording',
  data() {
    return {
      isRecording: false,
      mediaRecorder: null,
      recordedChunks: [],
      stream: null,
      videoUrl: "",
    };
  },
  computed: {
    videoSrc() {
      return this.stream ? this.$refs.videoRef.srcObject : null;
    },
  },
  mounted() {
    document.addEventListener("visibilitychange", this.handleVisibilityChange);
  },
  beforeUnmount() {
    document.removeEventListener("visibilitychange", this.handleVisibilityChange);
  },
  methods: {
    startRecording() {
      navigator.mediaDevices
        .getUserMedia({ video: true })
        .then((stream) => {
          this.$refs.videoRef.srcObject = stream;
          this.stream = stream;
          this.recordedChunks = [];
          this.mediaRecorder = new MediaRecorder(stream);
          this.mediaRecorder.addEventListener("dataavailable", (event) => {
            if (event.data.size > 0) {
              console.log(event.data.size);
              this.recordedChunks.push(event.data);
            }
          });
          this.mediaRecorder.start();
          this.isRecording = true;
        })
        .catch((error) => {
          console.error("Error accessing webcam:", error);
        });
    },
    stopRecording() {
      if (this.mediaRecorder && this.mediaRecorder.state === "recording") {
        this.mediaRecorder.addEventListener("stop", () => {
          const blob = new Blob(this.recordedChunks, { type: "video/webm" });
          this.videoUrl = URL.createObjectURL(blob);
        });

        this.mediaRecorder.stop();
        this.isRecording = false;
        this.stream.getTracks().forEach((track) => track.stop());
      }
      if (this.videoUrl) {
        const a = document.createElement("a");
        a.href = this.videoUrl;
        a.download = "webcam_video.webm";
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
      }
    },
    saveRecording() {
      if (this.videoUrl) {
        const a = document.createElement("a");
        a.href = this.videoUrl;
        a.download = "webcam_video.webm";
        document.body.appendChild(a);
        a.click();
        document.body.removeChild(a);
      }
    },
    // handleVisibilityChange() {
    //   if (document.visibilityState === "hidden") {
    //     // User switched tab or minimized the window
    //     // Stop recording if in progress
    //     if (this.isRecording) {
    //       this.stopRecording();
    //     }
    //   } else {
    //     // User switched back to the tab
    //     // Restart recording if needed
    //     if (this.stream && !this.isRecording) {
    //       this.startRecording();
    //     }
    //   }
    // },
  },
};
</script>


<!-- <template>
  <div class="btn">
    <button @click="startRecording">Start Recording</button>
    <button @click="stopRecording">Stop Recording</button>
    <button @click="saveRecording" :disabled="!isRecording">Save</button>
    <div class="camera-light" :class="{ active: isRecording }"></div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      mediaStream: null,
      mediaRecorder: null,
      recordedChunks: [],
      isRecording: false,
    };
  },
  methods: {
    async startRecording() {
      try {
        this.mediaStream = await navigator.mediaDevices.getUserMedia({
          video: true,
        });
        this.mediaRecorder = new MediaRecorder(this.mediaStream);
        this.mediaRecorder.addEventListener("dataavailable", (event) => {
          if (event.data.size > 0) {
            this.recordedChunks.push(event.data);
          }
        });
        this.mediaRecorder.start();
        this.isRecording = true;
      } catch (error) {
        console.error(error);
      } 
    }, 
    stopRecording() {
      if (this.mediaRecorder && this.mediaStream) {
        this.mediaRecorder.stop();
        this.mediaStream.getTracks().forEach((track) => track.stop());
        this.isRecording = false;
      }
    },
    saveRecording() {
      const blob = new Blob(this.recordedChunks, { type: "video/webm" });
      const url = URL.createObjectURL(blob);
      const a = document.createElement("a");
      a.href = url;
      a.download = "recorded_video.webm";
      document.body.appendChild(a);
      a.click();
      document.body.removeChild(a);
      URL.revokeObjectURL(url);

      this.recordedChunks = [];
    },
  },
};
</script>

<style>
.btn {
  margin-left: 90px;
}
.camera-light {
  width: 20px;
  height: 20px;
  background-color: red;
  border-radius: 50%;
  margin-bottom: 10px;
}

.camera-light.active {
  background-color: green;
}
</style> -->
<style>
.camera{
  background-color: #e4e9f7;
  padding-bottom: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.inner_section{
 
}
</style>