<template>
  <div class="home">
    <b-container>
      <b-row>
        <job-card v-for="job in displayJobs" :key="job.id" :name="job.name" />
      </b-row>
      <b-pagination
        v-model="currentPage"
        :total-rows="rows"
        :per-page="perPage"
        first-text="First"
        prev-text="Prev"
        next-text="Next"
        last-text="Last"
        v-on:input="paginate(currentPage)"
      ></b-pagination>
    </b-container>
  </div>
</template>

<script>
import JobCard from "../components/JobCard.vue";
import { mapGetters } from "vuex";

export default {
  name: "HomeView",
  components: { "job-card": JobCard },
  computed: {
    ...mapGetters(["jobs"]),
  },
  data() {
    return {
      // jobs: [],
      displayJobs: [],
      currentPage: 1,
      perPage: 3,
      rows: 1,
    };
  },
  methods: {
    async fetchData() {
      await this.$store.dispatch("fetchJobs");
      console.log(this.$store.getters.jobs);
      // fetch jobs
      // const res = await fetch("jobs.json");
      // const val = await res.json();
      // set 'jobs' data
      // this.jobs = this.jobs;
      this.displayJobs = this.jobs.slice(0, 3);
      console.log(this.jobs);
      // set pagination rows
      this.rows = this.jobs.length;
    },
    paginate(currentPage) {
      // arr manipulation for pagination
      const start = (currentPage - 1) * this.perPage;
      this.displayJobs = this.jobs.slice(start, start + this.perPage);
    },
  },
  created() {
    this.fetchData();
  },
};
</script>
