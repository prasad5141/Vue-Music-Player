<template>
<div>
    <ul>
      <li v-for="song in getSongs()" :key="song.id" @click="newestAudio()">
        {{song.name}}
        </li>
    </ul>
    <button @click="newestAudio()"> play</button>
</div>



</template>

<script>

// import a from "/assets/music/"

export default {
  name: 'App',
  data(){
    return {songsList:[
      {
        id:1,
        name:"DJ Tillu",
        path:"'@/music/2.mp3'"
      },
      { id:2,
        name:"Prematho",
        path:"@/music/1.mp3"
      }
    ]
    }
  },
  components: {
  },
  methods:{
        newestAudio() {
          // return "https://interactive-examples.mdn.mozilla.net/media/cc0-audio/t-rex-roar.mp3"
          // return '@/Prematho.mp3'
          // let p = ''
          let sound = ( new Audio( require('@/music/2.mp3') )).play()
          sound.play()
      },
      getSongs(){
        return this.songsList
      }

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
