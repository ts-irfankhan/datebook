# Recurrence Generator

The recurrence of an event is how often the event is supposed to occur. Some examples of this could be:

* an event that occurs once every Friday
* an event that occurs every other week
* an event that occurs daily for five days

Recurrence is **optional**.

<ClientOnly>
  <Recurrence />
  
  <h2>Result</h2>

  <h3>iCalendar RRULE</h3>

  <pre class="language-js"><RRule :data="filteredRecurrence" /></pre>

  <h3>Datebook Recurrence Object</h3>

  <pre class="language-js">{{ JSON.stringify(filteredRecurrence, null, 2) }}</pre>
</ClientOnly>