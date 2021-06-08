<template>
  <v-simple-table>
    <template v-slot:default>
      <thead>
        <tr>
          <th class="text-left">
            Улс
          </th>
          <th class="text-left">
            Нийт өвчилсөн
          </th>

          <th class="text-left">
            Нийт нас барсан
          </th>
          <th class="text-left">
            Нийт эдгэрсэн
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in Countries" :key="index">
          <td>{{ item.Country }}</td>
          <td>{{ item.TotalConfirmed }}</td>
          <td>{{ item.TotalDeaths }}</td>
          <td>{{ item.TotalRecovered }}</td>
        </tr>
      </tbody>
    </template>
  </v-simple-table>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      Countries: {}
    };
  },

  async created() {
    const config = {
      headers: {
        Accept: "application/json"
      }
    };
    try {
      const res = await axios.get("https://api.covid19api.com/summary", config);
      this.Countries = res.data.Countries;
      console.log(res.data);
    } catch (err) {
      console.log(err);
    }
  }
};
</script>
<style></style>
