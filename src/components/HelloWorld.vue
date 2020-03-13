<template>
  <div>
    <img src="https://covid19.mathdro.id/api/og" />
    <h2>Confirmed: {{ confirmed }}</h2>
    <h2>Deaths: {{ deaths }}</h2>

    <table>
      <thead>
        <tr>
          <td>State</td>
          <td>Region</td>
          <td>Last Update</td>
          <td>Latitude</td>
          <td>Longitude</td>
          <td>Confirmed</td>
          <td>Deaths</td>
          <td>Recovered</td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="detail in confirmedDetails" :key="detail.id">
          <td>{{ detail.provinceState }}</td>
          <td>{{ detail.countryRegion }}</td>
          <td>{{ detail.lastUpdate }}</td>
          <td>{{ detail.lat }}</td>
          <td>{{ detail.long }}</td>
          <td>{{ detail.confirmed }}</td>
          <td>{{ detail.deaths }}</td>
          <td>{{ detail.recovered }}</td>
        </tr>
      </tbody>
    </table>

    Source:
    <a href="https://github.com/mathdroid/covid-19-api"
      >https://github.com/mathdroid/covid-19-api</a
    >
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data: function() {
    return {
      confirmed: null,
      deaths: null,
      confirmedDetails: null
    };
  },
  mounted() {
    this.axios.get("https://covid19.mathdro.id/api").then(response => {
      this.confirmed = response.data.confirmed.value;
      this.deaths = response.data.deaths.value;
    });
    this.axios
      .get("https://covid19.mathdro.id/api/confirmed")
      .then(response => {
        console.table(response.data);
        this.confirmedDetails = response.data;
      });
  }
};
</script>
