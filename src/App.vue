<template>
<div>
  <div class="container">
    <div class="row">
      <div class="col-md-6">
         <ul class="list-group">
          <li v-for="(song, id) in getSongs()" :key="id" @click="playFromList(id)" class="list-group-item">
            {{song.name}}
          </li>
        </ul>
      </div>
        <div class="col-md-6">
            <div>
              <AVCircle
                :src="getCurrentSong()">
              </AVCircle>
            </div>
            <div>
                <button @click="playPrevious()" type="button" class="btn btn-outline-success">
                  Previous
                </button>
                <button @click="palyPauseAction(1)" type="button" class="btn btn-outline-success">
                  <div v-if="isPlayerRunning">
                    Pause
                  </div>
                  <div v-else>
                  play
                  </div>
                </button>
                
                <button @click="playNext()" type="button" class="btn btn-outline-success">
                  Next
                </button>
            </div>
          </div>
    </div>
  </div>
   


     
</div>



</template>

<script>

// import a from "/assets/music/"
import {  AVCircle } from 'vue-audio-visual'


export default {
  name: 'App',
  data(){
    return {
      audio:null,
      isPlayerRunning:false,
      currentSongID:null,
      currentSongSrc:"https://raw.githubusercontent.com/prasad5141/Vue-Music-Player/main/src/music/1.mp3",
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
    AVCircle
  },
  methods:{
    getCurrentSong(){
      return this.currentSongSrc
    },
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
          console.log(this.audio.duration)
      },
      getSongs(){
        return this.songsList
      },
      playFromList(songId){
        this.currentSongID = parseInt(songId)
        let path = "https://raw.githubusercontent.com/prasad5141/Vue-Music-Player/main/src/music/"+songId+".mp3"
        // console.log(path)
        // this.audio.src = path;
        // this.audio.play()
        this.currentSongSrc = path
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
body{
  background-color: rgb(223,231,239);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
li{
  background-color: rgb(240,240,240) !important;
}
canvas{
  display: none;
}
</style>
