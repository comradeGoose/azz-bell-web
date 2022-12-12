<template>
  <div class="about">
    <h1>This is an about page</h1>
    <button class="btn" @click="get_music_list">GET</button>

    <div v-for="music of music_list" :key="music">
      <button class="btn" @click="post_play_music(music)" value={{music}}> {{music}} </button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      music_list: null,
      music_play: null
    }
  },
  methods: {
    get_music_list: function () {
      axios.get('/music_list')
        .then((response) => {
          console.log(response)
          console.log(response.data)
          this.music_list = response.data
        })
        .catch(function (error) {
          console.log(error)
        })
    },
    post_play_music: function (music) {
      axios.post('/play_music', {
        play_music: music
      })
        .then((response) => {
          console.log(response)
        })
        .catch(function (error) {
          console.log(error)
        })
    },
    updateVolume: function (volume) {
      this.volume = volume
    }
  }
}
</script>
