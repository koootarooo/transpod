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
    <button class="translate_btn" @click="translate()">translate</button>
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
      console.log('translate')
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
</style>
