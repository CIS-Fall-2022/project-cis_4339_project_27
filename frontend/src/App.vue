<template>
  <main class="flex flex-row">
    <div id="_container" class="h-screen">
      <header class="w-full">
        <section class="text-center">
          <img class="m-auto" src="@\assets\DanPersona.svg" />
        </section>
        <nav class="mt-10">
          <ul class="flex flex-col gap-4">
            <li>
              <router-link to="/">
                <span style="position: relative; top: 6px" class="material-icons">dashboard</span>
                Dashboard
              </router-link>
            </li>
            <li>
              <router-link to="/intakeform">
                <span style="position: relative; top: 6px" class="material-icons">people</span>
                Client Intake Form
              </router-link>
            </li>
            <li>
              <router-link to="/eventform">
                <span style="position: relative; top: 6px" class="material-icons">event</span>
                Create Event
              </router-link>
            </li>
            <li>
              <router-link to="/findclient">
                <span style="position: relative; top: 6px" class="material-icons">search</span>
                Find Client
              </router-link>
            </li>
            <li>
              <router-link to="/findEvents">
                <span style="position: relative; top: 6px" class="material-icons">search</span>
                Find Event
              </router-link>
            </li>
          </ul>
        </nav>
      </header>
    </div>
    <div class="grow w-4/5">
      <section
        class="justify-end items-center h-24 flex"
        style="
          background: linear-gradient(250deg, #398AD7 70%, #efecec 50.6%);
        "
      >
      <!--Lori Vo. want to change according to what organization is using database-->
        <h1 class="mr-20 text-3xl text-white">{{this.getHeader()}}</h1>
      </section>
      <div>
        <router-view></router-view>
      </div>
    </div>
  </main>
</template>

<script>
// import axios from 'axios';
// import moment from 'moment';
export default {
  name: "App",
  methods:{
  getHeader:function(){
    //https://vitejs.dev/guide/env-and-mode.html
    let getOrganization = import.meta.env.VITE_ORGANIZATION;
    return getOrganization;
  }},
  components: {

  },
  // data() {
  //   return{
  //   clients: [],
  //   events: []
  //   }
  // },
  // async created() {
  //   const {data} = await axios.get('http://localhost:3000/eventData/recentEvent/')

  //   data.forEach(d => {
  //     const date = moment(d.date);
  //     // const date = moment(d.date, "YYYY-MMM-DD").format("MM/DD");

  //     const {
  //       eventName,
  //       attendees
  //     } = d;

  //     this.clients.push({date, total:attendees.length});
  //     this.events.push({date, total:eventName})
  //   console.log(this.clients)
      
  //   })
  // },
};
</script>

<style>
#_container {
  background-color: #2F66A9;
  color: white;
  padding: 18px;
}
</style>
