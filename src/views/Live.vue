<template>
  <div id="live">
    <div id="updates-container">
      <h1>Live Updates</h1>

      <div class="left-inner-container">
        <div v-for="message in $parent.messages">
          <span class="message-text">{{ message.text }}</span><br>
          <span class="message-time">{{ formatTime(message.created) }}</span>
          <hr>
        </div>
      </div>
    </div>

    <div id="schedule-container">
      <h1>Schedule</h1>
      
      <div class="center-inner-container">
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

    <div id="leaderboard-container">
      <h1>Leaderboard</h1>

      <div class="left-inner-container">
        <div v-for="(score, index) in scores" class="top-score">
          <h2>{{ index + 1 }}. {{ score.email }} - {{ score.points }}</h2>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import schedule from '../schedule.json';

  export default  {
    name: 'live',
    props: [],
    mounted() {

    },
    data() {
      return {
        schedule
      }
    },
    methods: {
      formatTime(time) {
        var datetime = new Date(time);
        var minutes = datetime.getMinutes();
        var hours = datetime.getHours();
        var ampm = "am";
        
        if (hours > 12) {
          hours -= 12;
          ampm = "pm";
        }

        if (minutes < 10) {
          minutes = "0" + minutes;
        }

        return hours + ":" + minutes +  " " + ampm;
      }
    },
    computed: {
      scores() {
        return this.$parent.scores
      }
    }
  }
</script>

<style scoped lang="scss">
  @import '@/globalVars.scss';

  #live {
    position: absolute;
    left: 0px;
    right: 0px;
    height: 90vh;
    padding: 20px;
  }

  #updates-container {
    background: $blue;
    position: relative;
    border-radius: 10px;
    border: 10px solid $blue;
    margin-bottom: 20px;
  }

  #schedule-container {
    background: $light-blue;
    position: relative;
    border-radius: 15px;
    border: 10px solid $light-blue;
    margin-bottom: 20px;
  }

  #leaderboard-container {
    background: $red;
    position: relative;
    border-radius: 15px; 
    border: 10px solid $red;
    margin-bottom: 20px;
  }

  .center-inner-container {
    background: white;
    padding: 10px;
    height: 80%;
    text-align: center;
    overflow-y: scroll;
  }

  .left-inner-container {
    background: white;
    padding: 10px;
    height: 80%;
    text-align: left;
    overflow-y: scroll;
  }

  .event {
    margin-bottom: 0.8em;
  }

  div.day {
    width: 100%;
    padding-bottom: 0.5em;
  }

  div span {
    font-size: 1em;
    font-weight: bold;
  }

  h1 {
    font-size: 2em;
  }

  h2 {
    font-size: 1.5em;
    font-weight: bold;
  }

  @media screen and (min-width: 700px) {
    .event {
      margin-bottom: 1.5em;
    }

    div span {
      font-size: 1.4em;
    }

    h1 {
      font-size: 40px;
    }

    h2 {
      font-size: 2em;
    }
  }

  @media screen and (min-width: 1240px) {
    #live {
      display: grid;
      grid-template-columns: 33% 40% 25%;
      grid-template-rows: 50% 33% 15%;
      grid-column-gap: 1%;
      grid-row-gap: 1%;
    }

    #updates-container {
      height: 98%;
      grid-column: 1 / 1;
      grid-row: 1 / 4;
    }

    #schedule-container {
      height: 98%;
      grid-column: 2 / 2;
      grid-row: 1 / 4;
    }

    #leaderboard-container {
      height: 98%;
      grid-column: 3 / 3;
      grid-row: 1 / 4;
    }

    .center-inner-container {
      padding: 20px;
    }

    .left-inner-container {
      padding: 20px;
    }
  }
</style>
