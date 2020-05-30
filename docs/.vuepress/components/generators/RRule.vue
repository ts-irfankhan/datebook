<template>
  <div>
    <Recurrence v-model="config.recurrence" />
    
    <h2>Result</h2>

    <h3>iCalendar `RRULE`</h3>

    <pre class="language-js"><RRuleText :data="datebookConfig" /></pre>
    
    <h3>Datebook Recurrence Config Object</h3>

    <pre class="language-js">{{ JSON.stringify(datebookConfig, null, 2) }}</pre>
  </div>
</template>

<script>
import Recurrence from '../forms/Recurrence.vue'
import RRuleText from '../displays/RRuleText.vue'
import getFilteredRecurrence from '../../utils/getFilteredRecurrence'

export default {
  name: 'RRule',
  computed: {
    Recurrence,
    RRuleText
  },
  computed: {
    datebookConfig () {
      return getFilteredRecurrence(this.config.recurrence)
    }
  }
}
</script>