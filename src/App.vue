<template>
  <Navbar />
  <div class="divide">
    <div class="sub_division1"> 
      <Sidebar />
    </div>
    <div class="sub_division2"> 
      <Mainarea />
      <CameraRecording />
    </div>
  </div>
</template>

<script>
import Navbar from './components/Navbar'
import Sidebar from './components/Sidebar'
import Mainarea from './components/Mainarea.vue'
import CameraRecording from './components/CameraRecording.vue'

export default {
  name: 'App',
  components: {
    Navbar,
    Sidebar,
    Mainarea,
    CameraRecording
  }
}
</script>

<style>
.divide{
  display: flex;

}
.sub_division1{
  /* display: flex; */
  flex-basis: 5%;
  /* display:fixed; */
}
.sub_division2{
  /* display: flex; */
  flex-basis: 95%;
}

</style>
