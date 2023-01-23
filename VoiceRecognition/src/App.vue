
<template>

  <div class="app">
    <button @click="ToggleMic" :class="`mic`">
      <span v-if="!isRecording" class="material-icons">
        mic
        </span>
      <span v-else class="material-icons">
        mic_off
        </span>
    </button>
    <div class="transcript" v-text="transcript"></div>
  </div>

</template>


<script setup>
  import { ref, onMounted } from 'vue'

  const transcript = ref('')
  const isRecording = ref(false)

  const Recognition = window.SpeechRecognition || window.webkitSpeechRecognition
  const sr =  new Recognition()

  onMounted(() => {
    sr.continuos = true
    sr.interimResults = true

    sr.onstart = () => {
      console.log('SR started');
      isRecording.value = true
    }

    sr.onend = () => {
      console.log('SR Stopped');
      isRecording.value = false
    }

    sr.onresult = (evt) => {
      // console.log(evt);
      const t = Array.from(evt.results)
        .map(result => result[0])
        .map(result => result.transcript)
        .join('')

      transcript.value = t
    }
  })

  const ToggleMic = () => {
    if (isRecording.value) {
      sr.stop()
    } else {
      sr.start()
    }
  }
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Fira Sans', sans-serif;
}

body {
  background: #281936;
  color: #fff;
  padding: 30px;
  
}

.app {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

button {
  outline: none;
  border: none;
  cursor: pointer;
  margin: 50px;
  width: 50px;
  height: 50px;
  border-radius: 50%;
}

</style>
