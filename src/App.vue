<template>
  <v-app>
    <v-app-bar app color="secondary" light>
      <div class="d-flex align-center">
        <h2>SpaceX Launch</h2>
      </div>

      <v-spacer></v-spacer>
    </v-app-bar>

    <v-content>
      <v-container>
        <v-timeline v-if="launches.length > 0">
          <LaunchTimlineItem
            v-for="launch in launches"
            :key="launch.flight_number"
            :launch="launch"
          />
        </v-timeline>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
import axios from "axios";
import LaunchTimlineItem from "./components/LaunchTimeLineItem.vue";
export default {
  name: "App",
  components: {
    LaunchTimlineItem,
  },
  data: () => ({
    launches: [],
  }),
  async created() {
    const { data } = await axios.get(
      "https://api.spacexdata.com/v3/launches/past"
    );
    
    data.forEach((launch) => {
      this.launches.push(launch);
    });
  },
};
</script>
