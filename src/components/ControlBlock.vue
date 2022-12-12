<template>
    <div class="ControlBlock" @click="get_item">
        <ListLessonCall
        v-bind:call_list="call_list"
        @SetPlay="SetPlay"
        @deleteCall="deleteCall"
        @update_music_name="update_music_name"
        @update_time_start="update_time_start"
        @update_time_end="update_time_end"
        @update_week_days="update_week_days"
        />
        <br>
        <AddLessonCall @Add-LessonCall="AddLessonCall"/>
        <br>
    </div>
</template>

<script>
import axios from 'axios'
import ListLessonCall from '@/components/Lesson/ListLessonCall.vue'
import AddLessonCall from '@/components//Lesson/AddLessonCall.vue'

export default {
  data () {
    return {
      call_list: []
    }
  },

  components: {
    ListLessonCall,
    AddLessonCall
  },

  mounted () {
    axios.get('/ListLessonCall')
      .then((response) => {
        console.log(response.data)
        this.call_list = response.data
        // this.call_list.push(response.data)
      })
      .catch(function (error) {
        console.log(error)
      })
  },

  methods: {
    AddLessonCall (LessonCall) {
      this.call_list.push(LessonCall)
      axios.post('/set_calls', {
        call_list: this.call_list
      })
        .then((response) => {
          console.log(response)
        })
        .catch(function (error) {
          console.log(error)
        })
    },

    SetPlay: function (id) {
      this.call_list = this.call_list.map(t => t.id === id ? { ...t, play: !t.play } : t)
      axios.post('/set_calls', {
        call_list: this.call_list
      })
        .then((response) => {
          console.log(response)
        })
        .catch(function (error) {
          console.log(error)
        })
    },

    update_music_name: function (id, newValue) {
      this.call_list = this.call_list.map(t => t.id === id ? { ...t, music_name: newValue } : t)
      console.log(this.call_list)
    },

    update_time_start: function (id, newValue) {
      this.call_list = this.call_list.map(t => t.id === id ? { ...t, time_start: newValue } : t)
      console.log(this.call_list)
    },

    update_time_end: function (id, newValue) {
      this.call_list = this.call_list.map(t => t.id === id ? { ...t, time_end: newValue } : t)
      console.log(this.call_list)
    },

    update_week_days: function (id, newValue) {
      this.call_list = this.call_list.map(t => t.id === id ? { ...t, week_days: newValue } : t)
      console.log(this.call_list)
    },

    deleteCall: function (id) {
      this.call_list = this.call_list.filter(t => t.id !== id)
      axios.post('/set_calls', {
        call_list: this.call_list
      })
        .then((response) => {
          console.log(response)
        })
        .catch(function (error) {
          console.log(error)
        })
    }
  }
}
</script>

<style scoped>
.ControlBlock {
  max-width: 750px;
  width: 90%;
  margin: 0;
  padding: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
}
h2 {
    margin: 0;
    margin-bottom: 5px;
}
</style>
