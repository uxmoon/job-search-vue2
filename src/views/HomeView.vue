<template>
  <div class="home">
    <b-container>
      <b-row>
        <job-card v-for="job in jobs" :key="job.id" :name="job.name" />
      </b-row>
      <b-pagination
        v-model="currentPage"
        :total-rows="rows"
        :per-page="perPage"
        first-text="First"
        prev-text="Prev"
        next-text="Next"
        last-text="Last"
      ></b-pagination>
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
      currentPage: 1,
      perPage: 3,
      rows: 1,
    };
  },
  methods: {
    async fetchData() {
      // fetch jobs
      const res = await fetch("jobs.json");
      const val = await res.json();
      // set 'jobs' data
      this.jobs = val;
      console.log(val);
      // set pagination rows
      this.rows = this.jobs.length;
    },
  },
  created() {
    this.fetchData();
  },
};
</script>
