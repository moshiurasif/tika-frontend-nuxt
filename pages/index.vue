<template>
  <h2 v-if="apiValue">{{ apiValue }}</h2>
  <h2 v-else>Loading....</h2>
</template>

<script>
export default {
  data() {
    return {
      apiValue: "",
    };
  },
  mounted() {
    this.getDataFromApi();
  },
  methods: {
    getDataFromApi() {
      this.$axios.get("http://127.0.0.1:8000/api").then((res) => {
        console.log(res.data);
        this.apiValue = res.data;
      });
    },
  },
};
</script>
