<template>
    <li>
        <div class="content">
            <button class="btn_ok" @click="$emit('SetPlay', call.id)">
              <h1 v-if=!call.play>||</h1>
              <h1 v-else>▶</h1>
            </button>
            <div class="container">
                <div class="content_item">
                  <select class="selected_music_list" v-model="selected" @change="$emit('update_music_name', call.id, selected)">
                    <option disabled value="">Please select one</option>
                    <option v-for="music of music_list" :key="music">{{music}}</option>
                  </select>
                    <input type="time" name="" id="" v-model="time_start" @input="$emit('update_time_start', call.id, time_start)">
                    <h1>|</h1>
                    <input type="time" name="" id="" v-model="time_end" @input="$emit('update_time_end', call.id, time_end)">
                </div>
                <div class="content_item">
                    <input class="checkbox" type="checkbox" id="Monday" value="1" v-model="checked_week_days" @change="$emit('update_week_days', call.id, checked_week_days)">
                    <label for="jack">Пн</label>
                    <input class="checkbox"  type="checkbox" id="Tuesday" value="2" v-model="checked_week_days" @change="$emit('update_week_days', call.id, checked_week_days)">
                    <label for="john">Вт</label>
                    <input class="checkbox"  type="checkbox" id="Wednesday" value="3" v-model="checked_week_days" @change="$emit('update_week_days', call.id, checked_week_days)">
                    <label for="mike">Ср</label>
                    <input class="checkbox"  type="checkbox" id="Thursday" value="4" v-model="checked_week_days" @change="$emit('update_week_days', call.id, checked_week_days)">
                    <label for="mike">Чт</label>
                    <input class="checkbox"  type="checkbox" id="Friday" value="5" v-model="checked_week_days" @change="$emit('update_week_days', call.id, checked_week_days)">
                    <label for="mike">Пт</label>
                    <input class="checkbox"  type="checkbox" id="Saturday" value="6" v-model="checked_week_days" @change="$emit('update_week_days', call.id, checked_week_days)">
                    <label for="mike">Сб</label>
                    <input class="checkbox"  type="checkbox" id="Sunday" value="0" v-model="checked_week_days" @change="$emit('update_week_days', call.id, checked_week_days)">
                    <label for="mike">Вс</label>
                </div>
            </div>
            <button class="btn_ok" @click="$emit('deleteCall', call.id)">
              <h1> × </h1>
            </button>
        </div>
    </li>
  </template>

<script>
import axios from 'axios'
// import { ref } from 'vue'
// const selected = ref('A')
// const selected = ref(this.call.music_name)
export default {
  props: {
    call: {
      type: Object,
      required: true
    },
    index: Number
  },
  data () {
    return {
      selected: this.call.music_name,
      time_start: this.call.time_start,
      time_end: this.call.time_end,
      checked_week_days: this.call.week_days,
      music_list: [
        '123',
        '456'
      ]
    }
  },
  mounted () {
    axios.get('/music_list')
      .then((response) => {
        console.log(response.data)
        this.music_list = response.data
      })
      .catch(function (error) {
        console.log(error)
      })
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
    log_checkedNames () {
      console.log(this.checkedNames)
    }
  }
}

</script>

<style scoped>
.btn_ok {
    width: 50px;
    height: 50px;
    border-radius: 1rem;
    border-color: #2896ea;
    background-color: #2896ea;
    margin: 0;
    padding: 0;
}

.content {
    display: flex;
    align-content: center;
    flex-direction: row;
    align-items: center;
    justify-content: center;
}

.content_item {
    display: flex;
    align-content: space-around;
    justify-content: space-evenly;
    flex-direction: row;
    align-items: center;
    margin-left: 5px;
    margin-right: 5px;
}

.container {
    min-width:max-content;
}

.selected_music_list {
  color: #2896ea;
  background-color: rgba(255, 255, 255, 0);
}

li {
    width: 400px;
    height: auto;
    border: 2px solid #2896ea;
    border-radius: 1rem;
    background-color: rgba(0, 221, 255, 0.106);
    display: inline-block;
    align-items: center;
    margin: 0 0 10px 0;
}

h1 {
    margin: 0;
    padding: 0;
}

input[type="time" i] {
    color: #2896ea;
    background-color: rgba(255, 255, 255, 0);
}

[type=time] {
  max-width: 80px;
}

select {
  max-width: 125px;
}
</style>
