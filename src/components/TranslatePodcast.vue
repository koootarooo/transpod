<template>
  <div class="translate">
    <div class="msg">
      <h1>{{ msg }}</h1>
    </div>
    <div class="drop_zone" @dragenter="dragEnter" @dragleave="dragLeave" @dragover.prevent @drop.prevent="dropFile" :class="{enter: isEnter}">
      <img src="../assets/upload_img.png" width="60" height="60">
      Drag & drop to upload
    </div>
    <div class="preview_zone">
      <p>{{file_title}}</p>
      <p>{{file_size}}</p>
    </div>
    <button class="translate_btn" @click="translate()" v-if="!isLoading">translate</button>
    <div class="loading_contents" v-if="isLoading">
      <div class="loading_message">
        Now Translating...<br>
        We'll send you email when tlanslating is done.
      </div>
      <div class="fulfilling-bouncing-circle-spinner">
        <div class="circle"></div>
        <div class="orbit"></div>
      </div>
      <div class="translate_more" @click="reset()">
        <span class="translate_again_btn">translate another file</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TranslatePodcast',
  props: {
    msg: String
  },
  data() {
    return {
      file_title: "",
      file_size: "",
      isEnter: false,
      isLoading: false
    }
  },
  methods: {
    dragEnter() {
      this.isEnter = true;
    },
    dragLeave() {
      this.isEnter = false;
    },
    dropFile() {
      const file = event.dataTransfer.files[0]
      this.file_title = file.name
      const fs = file.size/1024/1024
      this.file_size = fs.toFixed(1) + "MB"
      this.isEnter = false;
    },
    translate() {
      this.isLoading = true
    },
    reset() {
      this.file_title = ""
      this.file_size = ""
      this.isLoading = false
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.translate {
  height: 100%;
  width: 100%;
  display: flex;
  flex-direction: column;
}
.msg {
  align-self: center;
}
.upload_zone {
  align-self: center;
}
.drop_zone {
  border: 3px dotted #d3d3d3;
  width: 50vw;
  height: 20vw;
  display:flex;
  align-self: center;
  flex-flow: column;
  align-items: center;
  justify-content: center;
  color: black;
  font-size: 20px;
  font-weight: bold;
}
.drop_zone p {
  color: black;
  font-size: 20px;
}
.enter {
  background-color:  rgb(26, 94, 240);
  opacity: 0.3;
}
.translate_btn {
  display: block;
	text-align: center;
	text-decoration: none;
	width: 250px;
	margin: auto;
	padding: 1rem 4rem;
  font-size: 20px;
	font-weight: bold;  
	border: 2px solid #27acd9;
	background: #27acd9;
	color: #fff;
	border-radius: 100vh;
	transition: 0.5s;
}
.translate_btn:hover {
	color: #27acd9;
	background: #fff;
}
.loading_contents {
  display: flex;
  align-self: center;
  flex-flow: column;
  align-items: center;
  justify-content: center;
}
.loading_message {
  padding-bottom: 20px;
  font-weight: bold;
}
.translate_more {
  padding-top: 20px;
}
.translate_again_btn {
  text-decoration: underline;
  color: blue;
}
/* 以下アニメーション */
.fulfilling-bouncing-circle-spinner, .fulfilling-bouncing-circle-spinner * {
  box-sizing: border-box;
}

.fulfilling-bouncing-circle-spinner {
  height: 60px;
  width: 60px;
	display: flex;
  align-self: center;
  animation: fulfilling-bouncing-circle-spinner-animation infinite 4000ms ease;
}

.fulfilling-bouncing-circle-spinner .orbit {
  height: 60px;
  width: 60px;
  position: absolute;
  top: 0;
  left: 0;
  border-radius: 50%;
  border: calc(60px * 0.03) solid #27acd9;
  animation: fulfilling-bouncing-circle-spinner-orbit-animation infinite 4000ms ease;
}

.fulfilling-bouncing-circle-spinner .circle {
  height: 60px;
  width: 60px;
  color: #27acd9;
  display: block;
  border-radius: 50%;
  position: relative;
  border: calc(60px * 0.1) solid #27acd9;
  animation: fulfilling-bouncing-circle-spinner-circle-animation infinite 4000ms ease;
  transform: rotate(0deg) scale(1);
}

@keyframes fulfilling-bouncing-circle-spinner-animation {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
  }

@keyframes fulfilling-bouncing-circle-spinner-orbit-animation {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1);
  }
  62.5% {
    transform: scale(0.8);
  }
  75% {
    transform: scale(1);
  }
  87.5% {
    transform: scale(0.8);
  }
  100% {
    transform: scale(1);
  }
}

@keyframes fulfilling-bouncing-circle-spinner-circle-animation {
  0% {
    transform: scale(1);
    border-color: transparent;
    border-top-color: inherit;
  }
  16.7% {
    border-color: transparent;
    border-top-color: initial;
    border-right-color: initial;
  }
  33.4% {
    border-color: transparent;
    border-top-color: inherit;
    border-right-color: inherit;
    border-bottom-color: inherit;
  }
  50% {
    border-color: inherit;
    transform: scale(1);
  }
  62.5% {
    border-color: inherit;
    transform: scale(1.4);
  }
  75% {
    border-color: inherit;
    transform: scale(1);
    opacity: 1;
  }
  87.5% {
    border-color: inherit;
    transform: scale(1.4);
  }
  100% {
    border-color: transparent;
    border-top-color: inherit;
    transform: scale(1);
  }
} 
</style>
