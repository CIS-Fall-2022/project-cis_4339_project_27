<template>
  <main>
    <div>
      <h1 class="font-bold text-4xl text-red-700 tracking-widest text-center mt-10">Welcome</h1>
      <!-- <canvas id="myChart" width="400" height="400"></canvas> -->
                  <AttendanceBar
              v-if="!loading && !error"
              :label="labels"
              :chart-data="attending"
            ></AttendanceBar>
    </div>
  </main>
</template>
<script>
// import Chart from 'chart.js/auto';
// import axios from 'axios';
// import moment from 'moment';
// //  import LineChart from "../components/LineChart"


// export default {
//   methods: {
//     routePush(routeName) {
//       this.$router.push({ name: routeName });
//     },
//      getData(){
//   var url = 'http://localhost:3000/eventData/recentEvent/'
//   var headers = {
//     'Content-Type': 'application/json'
//   }
//   axios.get(url,headers)
//   .then((x)=>{
//     // console.log(x.data)
//     var results = x.data
//     var events = []
//     var attendants = []

//     for (var i = 0; i < results.length; i++) {
//       var t = results[i].eventName
//       var y = results[i].attendees.length
//       events.push(t)
//       attendants.push(y)
//     }
//     this.eventName = events
//     this.attendees = attendants
//     var getEvents = Object.values(this.eventName)
//     var getAtten = Object.values(this.attendees)
//     console.log(this.eventName)
//     console.log(this.attendees)
//     console.log(getEvents)
//     console.log(getAtten)
//     return getEvents, getAtten
//   })
//  }

//   },
//     data() {
//     return{
//     eventName: [],
//     attendees: []
//     }
//   },
  // async created() {
  //   const {data} = await axios.get('http://localhost:3000/eventData/recentEvent/')

  //   data.forEach(d => {
  //     const event = d.event;
  //     // const date = moment(d.date, "YYYY-MMM-DD").format("MM/DD");

  //     const {
  //       eventName,
  //       attendees
      
  //     } = d;

   

  //     this.events.push({event:eventName,total: attendees.length })

  //   console.log(this.events)
   
      
  //   })
  // },

import axios from "axios";
import AttendanceBar from "@/components/BarChart.vue";

export default {
  components: {
    AttendanceBar,
  },
  data() {
    return {
      labels: [],
      attending: [],
      count: [],
      loading: false,
      error: null,
    };
  },
  methods: {
    async fetchData() {
      try {
        this.error = null;
        this.loading = true;
        const url = `http://localhost:3000/eventData/recentEvent/`;
        const response = await axios.get(url);
        //"re-organizing" - mapping json from the response
        this.labels = response.data.map((event) => event.eventName);
        this.attending = response.data.map((event) => event.attendees.length);
      } catch (err) {
        if (err.response) {
          // client received an error response (5xx, 4xx)
          this.error = {
            title: "Server Response",
            message: err.message,
          };
        } else if (err.request) {
          // client never received a response, or request never left
          this.error = {
            title: "Unable to Reach Server",
            message: err.message,
          };
        } else {
          // There's probably an error in your code
          this.error = {
            title: "Application Error",
            message: err.message,
          };
        }
      }
      this.loading = false;
    },
  },
  mounted() {
    this.fetchData();
  },
};

</script>


  
