<template>
<div>
    <ul>
      <li v-for="(song, id) in getSongs()" :key="id" @click="playFromList(id)">
        {{song.name}}
        </li>
    </ul>
    <button @click="playPrevious()">
      Previous
    </button>
    <button @click="palyPauseAction(1)">
      <div v-if="isPlayerRunning">
        Pause
      </div>
      <div v-else>
       play
       </div>
    </button>
    
    <button @click="playNext()">
      Next
    </button>
</div>



</template>

<script>

// import a from "/assets/music/"

export default {
  name: 'App',
  data(){
    return {
      audio:null,
      isPlayerRunning:false,
      currentSongID:null,
      songsList:{
        1:{
            name:"Prematho",
            path:"https://raw.githubusercontent.com/prasad5141/Vue-Music-Player/main/src/music/1.mp3"
          },
        2:{
            name:"DJ Tillu",
            path:"https://raw.githubusercontent.com/prasad5141/Vue-Music-Player/main/src/music/2.mp3"
          },
        3:{
          name:"Love Debba",
          path:"https://raw.githubusercontent.com/prasad5141/Vue-Music-Player/main/src/music/3.mp3"
        },

      }
      
    
    }
  },
  components: {
  },
  methods:{
        palyPauseAction(songId) {
          if (this.currentSongID === null){
            this.currentSongID = parseInt(songId)
            let path = "https://raw.githubusercontent.com/prasad5141/Vue-Music-Player/main/src/music/"+songId+".mp3"
            this.audio.src = path;
          }else{
            let path = "https://raw.githubusercontent.com/prasad5141/Vue-Music-Player/main/src/music/"+this.currentSongID+".mp3"
            this.audio.src = path;
          }          
          if (!this.isPlayerRunning){
            this.audio.play()
            this.isPlayerRunning = true;
          }else{
            this.audio.pause()
            this.isPlayerRunning = false;
          }
      },
      getSongs(){
        return this.songsList
      },
      playFromList(songId){
        this.currentSongID = parseInt(songId)
        let path = "https://raw.githubusercontent.com/prasad5141/Vue-Music-Player/main/src/music/"+songId+".mp3"
        console.log(path)
        this.audio.src = path;
        this.audio.play()
        this.isPlayerRunning = true;
        
      },
      playPrevious(){
        let songID = this.currentSongID-1
        let songIdList = Object.keys(this.songsList);
        console.log(songIdList,songID.toString())
        if (songIdList.includes(songID.toString())){
          this.playFromList(songID)
        }else{
          console.log(songID)
        }
      },
      playNext(){
        let songID = this.currentSongID+1
        let songIdList = Object.keys(this.songsList);
        console.log(songIdList,songID.toString())
        if (songIdList.includes(songID.toString())){
          this.playFromList(songID)
        }else{
          console.log(songID)
        }
      }

  },
  created(){
     this.audio = new Audio(  )
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
