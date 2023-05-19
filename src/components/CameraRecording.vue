<template>
    <div>
      <video ref="videoElement" autoplay></video>
      <button @click="startRecording" v-if="!isRecording">Start Recording </button>
      <button @click="stopRecording" v-if="isRecording">Stop Recording    </button>
    </div>
  </template>
  
  <script>
  export default {
    name:'CameraRecording',
    data() {
      return {
        mediaRecorder: null,
        recordedChunks: [],
        isRecording: false,
      };
    },
    mounted() {
      this.initializeCamera();
    },
    methods: {
      async initializeCamera() {
        try {
          const stream = await navigator.mediaDevices.getUserMedia({ video: true });
          this.$refs.videoElement.srcObject = stream;
          this.mediaRecorder = new MediaRecorder(stream);
  
          this.mediaRecorder.addEventListener('dataavailable', (event) => {
            if (event.data.size > 0) {
              this.recordedChunks.push(event.data);
            }
          });
  
          this.mediaRecorder.addEventListener('stop', () => {
            const blob = new Blob(this.recordedChunks, { type: 'video/webm' });
            const url = URL.createObjectURL(blob);
            console.log('Recorded video:', url);
            this.recordedChunks = [];
          });
        } catch (error) {
          console.error('Error accessing camera:', error);
        }
      },
      startRecording() {
        this.recordedChunks = [];
        this.mediaRecorder.start();
        this.isRecording = true;
      },
      stopRecording() {
        this.mediaRecorder.stop();
        this.isRecording = false;
      },
    },
  };
  </script>
  