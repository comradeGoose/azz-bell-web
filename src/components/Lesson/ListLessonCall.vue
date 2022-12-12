<template>
    <ul>
      <LessonCall
      v-for="(call, i) of call_list" :key="call.id"
      v-bind:call="call"
      v-bind:index="i"
      v-on:SetPlay="SetPlay"
      v-on:deleteCall="deleteCall"
      v-on:update_music_name="update_music_name"
      v-on:update_time_start="update_time_start"
      v-on:update_time_end="update_time_end"
      v-on:update_week_days="update_week_days"
      />
    </ul>
</template>

<script>
import LessonCall from '@/components/Lesson/LessonCall.vue'
export default {
  props: ['call_list'],
  components: {
    LessonCall
  },
  methods: {
    SetPlay (id) {
      this.$emit('SetPlay', id)
    },
    deleteCall (id) {
      this.$emit('deleteCall', id)
    },
    update_music_name (id, newValue) {
      this.$emit('update_music_name', id, newValue)
    },
    update_time_start (id, newValue) {
      this.$emit('update_time_start', id, newValue)
    },
    update_time_end (id, newValue) {
      this.$emit('update_time_end', id, newValue)
    },
    update_week_days (id, newValue) {
      this.$emit('update_week_days', id, newValue)
    }
  }
}
</script>

<style scoped>
ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
    display: flex;
    flex-direction: column;
    align-items: center;
}
</style>
