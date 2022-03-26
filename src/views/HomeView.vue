<template>
  <div class="home">
    <b-container>
      <b-row>
        <job-card v-for="job in jobs" :key="job.id" :name="job.name" />
      </b-row>
    </b-container>
  </div>
</template>

<script>
import JobCard from "../components/JobCard.vue";

export default {
  name: "HomeView",
  components: { "job-card": JobCard },
  data() {
    return {
      jobs: [],
    };
  },
  methods: {
    async fetchData() {
      const res = await fetch("jobs.json");
      const val = await res.json();
      // console.log(val);
      this.jobs = val;
    },
  },
  created() {
    this.fetchData();
  },
};
</script>
