<template>
  <div id="schedule">
   <h1>Schedule</h1>
   <div class="flex-schedule">
     <div class="day" id="friday">
       <h2>Friday, September 27th</h2>
         <div class="event" v-for="event in schedule.fridayEvents" v-bind:key="event.id">
           <span class="name">{{ event.title }}</span><br>
           <span class="time">{{ event.startTime }}</span>
           <span v-if="event.location != ''"> | </span>
           <span class="location">{{ event.location }}</span>
           <span class="description">{{ event.description }}</span>
         </div>
     </div>

     <div class="day" id="saturday">
       <h2>Saturday, September 28th</h2>
         <div class="event" v-for="event in schedule.saturdayEvents" v-bind:key="event.id">
           <span class="name">{{ event.title }}</span><br>
           <span class="time">{{ event.startTime }}</span>
           <span v-if="event.location != ''"> | </span>
           <span class="location">{{ event.location }}</span>
           <span class="description">{{ event.description }}</span>
         </div>
     </div>

     <div class="day" id="sunday">
       <h2>Sunday, September 29th</h2>
         <div class="event" v-for="event in schedule.sundayEvents" v-bind:key="event.id">
           <span class="name">{{ event.title }}</span><br>
           <span class="time">{{ event.startTime }}</span>
           <span v-if="event.location != ''"> | </span>
           <span class="location">{{ event.location }}</span>
           <span class="description">{{ event.description }}</span>
         </div>
     </div>
   </div>
  </div>
</template>

<script>
import schedule from '../schedule.json';

export default {
  main: 'Main',
  data() {
    return {
      schedule
    }
  },
  methods: {},
  mounted() {},
};
</script>

<style scoped lang="scss">
  @import '@/globalVars.scss';

  #schedule {
    padding: 10px 15vw;
    background-color: $sand;
    text-align: left;
  }

  .event {
    margin-bottom: 1.5em;
  }

  div.day {
    width: 100%;
    padding-bottom: 1em;
  }

  div span {
    font-size: 1.2em;
    font-weight: bold;
  }

  h2 {
    font-size: 1.5em;
    font-weight: bold;
  }

  body {
    padding: 0;
    margin: 0;
    margin-bottom: 200px;
  }

  @media only screen and (min-width: 900px) {
    schedule {
      padding: 2rem 6rem;
      background-color: $sand;
    }

    .flex-schedule {
      display: flex;
      flex-wrap: wrap;
    }

    .day + .day {
      padding-left: 2%;
    }
    
    div.day {
      text-align: left;
      width: 32%;
      font-size: 1.2em;
    }
    
    h2 {
      font-size: 1.8em;
      font-weight: bold;
    }
  }
</style>