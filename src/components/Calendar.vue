<template>
  <div>
    <v-sheet tile height="6vh" color="grey lighten-3" class="d-flex align-center">
      <v-btn outlined small class="ma-4" @click="setToday">
        今日
      </v-btn>
      <v-btn icon @click="$refs.calendar.prev()">
        <v-icon>mdi-chevron-left</v-icon>
      </v-btn>
      <v-btn icon @click="$refs.calendar.next()">
        <v-icon>mdi-chevron-right</v-icon>
      </v-btn>
      <v-toolbar-title>{{ title }}</v-toolbar-title>
    </v-sheet>
    <v-sheet height="94vh">
      <v-calendar
        ref="calendar"
        v-model="value"
        type="month"
        :events="events"
        :event-color="getEventColor"
        locale="ja-jp"
        :day-format="timestamp => new Date(timestamp.date).getDate()"
        :month-format="timestamp => (new Date(timestamp.date).getMonth() + 1) + ' /'"
        @change="getEvents"
      ></v-calendar>
    </v-sheet>
  </div>
</template>

<script>
import moment from 'moment';

export default {
  data: () => ({
    events: [],
    value: moment().format('yyyy-MM-DD'),
  }),
  computed: {
    title() {
      return moment(this.value).format('yyyy年 MM月');
    },
  },
  methods: {
    setToday() {
      this.value = moment().format('yyyy-MM-DD');
    },
    getEvents() {
      const events = [
        {
          name: '会議',
          start: new Date('2020-08-03T10:00:00'), // 開始時刻
          end: new Date('2020-08-03T11:00:00'), // 終了時刻
          color: 'blue',
          timed: true, // 終日ならfalse
        },
        {
          name: '休暇',
          start: new Date('2020-08-04'),
          end: new Date('2020-08-04'),
          color: 'green',
          timed: false,
        },
        {
          name: '出張',
          start: new Date('2020-08-05'),
          end: new Date('2020-08-07'),
          color: 'cyan',
          timed: false,
        },
        {
          name: '飲み会',
          start: new Date('2020-08-06'),
          end: new Date('2020-08-06'),
          color: 'orange',
          timed: false,
        },
        {
          name: '打ち合わせ',
          start: new Date('2020-08-07T10:00:00'),
          end: new Date('2020-08-07T11:00:00'),
          color: 'cyan',
          timed: false,
        },
        {
          name: '振り返り',
          start: new Date('2020-08-07:11:00:00'),
          end: new Date('2020-08-07T12:00:00'),
          color: 'cyan',
          timed: false,
        },
        {
          name: '休暇',
          start: new Date('2020-09-07'),
          end: new Date('2020-09-11'),
          color: 'green',
          timed: false,
        },
      ];
      this.events = events;
    },
    getEventColor(event) {
      return event.color;
    },
  },
};
</script>
