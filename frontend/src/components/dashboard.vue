<template>
  <main>
    <div>
      <h1 class="font-bold text-4xl text-red-700 tracking-widest text-center mt-10">Welcome</h1>
      <canvas id="myChart" width="400" height="400"></canvas>
    </div>
  </main>
</template>
<script>
import Chart from 'chart.js/auto';
import axios from 'axios';
import moment from 'moment';
//  import LineChart from "../components/LineChart"


export default {
  methods: {
    routePush(routeName) {
      this.$router.push({ name: routeName });
    },
 getData(){
  var url = 'http://localhost:3000/eventData/recentEvent/'
  var headers = {
    'Content-Type': 'application/json'
  }
  axios.get(url,headers)
  .then((x)=>{
    // console.log(x.data)
    var results = x.data
    var events = []
    var attendants = []

    for (var i = 0; i < results.length; i++) {
      var t = results[i].eventName
      var y = results[i].attendees.length
      events.push(t)
      attendants.push(y)
    }
    this.eventName = events
    this.attendees = attendants
    var getEvents = Object.values(this.eventName)
    var getAtten = Object.values(this.attendees)
    console.log(this.eventName)
    console.log(this.attendees)
    console.log(getEvents)
    console.log(getAtten)
    return getEvents, getAtten
  })
 }
  },
    data() {
    return{
    eventName: [],
    attendees: []
    }
  },
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

async mounted() {
await this.getData()
console.log(this.getAtten)
const ctx = document.getElementById('myChart').getContext('2d');

  var myChart = new Chart(ctx, {
    type: 'bar',
    
    data: {
        labels: ['mixer', 'event2'],
        datasets: [{
            label: 'Event Attendance',
            data: [2,1] ,
            backgroundColor: [
                'rgba(255, 99, 132, 0.2)',
                'rgba(54, 162, 235, 0.2)',
                'rgba(255, 206, 86, 0.2)',
                'rgba(75, 192, 192, 0.2)',
                'rgba(153, 102, 255, 0.2)',
                'rgba(255, 159, 64, 0.2)'
            ],
            borderColor: [
                'rgba(255, 99, 132, 1)',
                'rgba(54, 162, 235, 1)',
                'rgba(255, 206, 86, 1)',
                'rgba(75, 192, 192, 1)',
                'rgba(153, 102, 255, 1)',
                'rgba(255, 159, 64, 1)'
            ],
            borderWidth: 1
        }]
    },
    options: {
        scales: {
            y: {
                beginAtZero: true
            }
        }
    }
});
  }
  
}
</script>


  
