<template>
  <q-page>
    <Bubble :forecast="data" />
    <div class="city">
      <img
        src="https://res.cloudinary.com/dutj1bbos/image/upload/c_scale,h_600/v1616111698/3042_mvl40f.jpg"
        alt=""
      />
    </div>

    <div class="display: flex">
      <Days :forecast="data" width="250" height="96" />
      <City />
      <Reviews />
      <Location width="250" height="96" />
    </div>
  </q-page>
</template>

<script>
import Days from "./../components/Days";
import Bubble from "./../components/Bubble";
// import City from "./../components/City";
import Reviews from "./../components/Reviews";
import Location from "./../components/Location";
export default {
  data() {
    return {
      forecast: [],
      data: []
    };
  },
  components: {
    Days,
    Bubble,
    // City,
    Reviews,
    Location
  },
  created() {
    this.getData();
    this.filterDays();
    var Xmas95 = new Date("December 25, 1995 23:15:30");
    var weekday = Xmas95.getDay();
  },
  methods: {
    getData() {
      var data = this;
      var xhr = new XMLHttpRequest();
      var url =
        "http://api.openweathermap.org/data/2.5/forecast?q=bogota&units=metric&mode=json&appid=080ec8560a4965f95a43f80be54bae5d";
      xhr.open("GET", url, false);
      xhr.onreadystatechange = function() {
        if (this.readyState === XMLHttpRequest.DONE) {
          if (this.status === 200) {
            data = this.responseText;
          } else {
            console.log(this.status, this.statusText);
          }
        }
      };
      xhr.send();
      this.forecast = JSON.parse(data);
    },
    filterDays() {
      const groupedData = this.forecast.list.reduce((days, row) => {
        const date = row.dt_txt.split(" ")[0];
        days[date] = [...(days[date] ? days[date] : []), row];
        return days;
      }, {});
      console.log(groupedData);
      var i = 0;
      for (let date of Object.keys(groupedData)) {
        let wheater = groupedData[Object.keys(groupedData)[i]][i]["weather"][0];
        let date = Object.keys(groupedData)[i];
        i++;
        let arr = {
          tem_max: getMax(groupedData[date], "temp_max"),
          tem_min: getMin(groupedData[date], "temp_min"),
          humidity: getMax(groupedData[date], "humidity"),
          wheater,
          date
        };
        this.data.push(arr);
        console.log(this.data);
      }
      function getMax(arr, attr) {
        return Math.max.apply(
          Math,
          arr.map(item => item.main[attr])
        );
      }

      function getMin(arr, attr) {
        return Math.min.apply(
          Math,
          arr.map(item => item.main[attr])
        );
      }
    }
  }
};
</script>
