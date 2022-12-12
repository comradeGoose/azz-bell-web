<template>
    <div class="ControlBlock" @click="get_item">
        <ListLessonCall
        v-bind:call_list="call_list"
        @SetPlay="SetPlay"
        @deleteCall="deleteCall"
        @updateValue="updateValue"
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
      call_list: [
        {
          id: 0,
          play: false,
          music_name: 'Bonnie Tyler - Holding Out For a Hero.mp3',
          week_days: ['1', '2', '3', '4', '5', '6'],
          time_start: '08:00',
          time_end: '08:40'
        },
        {
          id: 1,
          play: true,
          music_name: 'The Mike Flowers Pops - Wonderwall.mp3',
          week_days: ['3', '6'],
          time_start: '13:30',
          time_end: ''
        }
      ]
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

    updateValue: function (id, value, newValue) {
      this.call_list = this.call_list.map(t => t.id === id ? { ...t, value: t.newValue } : t)
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
