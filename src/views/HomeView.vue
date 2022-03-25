<template>
  <div class="home">
    <b-container>
      <b-row>
        <b-col md="6" lg="3">
          <job-card />
        </b-col>
        <b-col md="6" lg="3">
          <job-card />
        </b-col>
        <b-col md="6" lg="3">
          <job-card />
        </b-col>
        <b-col md="6" lg="3">
          <job-card />
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import JobCard from "../components/JobCard.vue";

export default {
  name: "HomeView",
  components: { "job-card": JobCard },
};
</script>
