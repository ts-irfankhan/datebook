<template>
  <div>
    <dates
      v-model="config"
      :allday="allday"
    />
    <input
      v-model="allday"
      type="checkbox"
      id="allday"
      value="true"
    />
    <label for="allday">This is an all-day event</label>

    <h2>Recurrence</h2>

    <input
      v-model="recurs"
      type="checkbox"
      id="recurs"
      value="true"
    />
    <label for="recurs">This event repeats</label>

    <recurrence
      v-if="recurs"
      v-model="config.recurrence"
    />
    
    <h2>Result</h2>

    <h3>Google Calendar URL</h3>

    <pre class="language-js">{{ googleCalendarUrl }}</pre>

    <h3>Datebook Config Object</h3>

    <pre class="language-js">{{ JSON.stringify(datebookConfig, null, 2) }}</pre>
  </div>
</template>

<script>
import Dates from '../forms/Dates.vue'
import Recurrence from '../forms/Recurrence.vue'
import { GoogleCalendar } from '../../../../src'
import getFilteredRecurrence from '../../utils/getFilteredRecurrence'

export default {
  name: 'Calendars',
  components: {
    Dates,
    Recurrence
  },
  data () {
    return {
      allday: true,
      recurs: false,
      config: {
        title: '',
        description: '',
        start: (new Date()).toISOString().replace(/\.[0-9]+Z$/, ''),
        end: '',
        recurrence: {
          frequency: 'DAILY',
          interval: 1,
          month: 1,
          weekdays: [],
          monthdays: [],
          until: '',
          count: 1,
          byType: {
            weekdays: false,
            monthdays: false
          },
          byRepeat: {
            untilDate: false,
            count: false
          }
        }
      }
    }
  },
  computed: {
    datebookConfig () {
      const config = {
        ...this.config,
        recurrence: getFilteredRecurrence(this.config.recurrence)
      }

      if (this.allday) {
        delete config.end
      }

      if (!this.recurs) {
        delete config.recurrence
      }

      return config
    },
    googleCalendarUrl () {
      const googleCalendar = new GoogleCalendar(this.datebookConfig)

      return googleCalendar.render()
    }
  }
}
</script>