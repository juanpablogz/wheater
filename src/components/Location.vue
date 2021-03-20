<template>
  <div>
    <div>
      <div v-for="wheater in oneDay" :key="wheater.id" >
          <div class="elevate location">
            <div class="icon-top">
              <div class="container-wheater">
                <div class="temperature wheater-card">
                  <div>
                    <img src="http://openweathermap.org/img/w/10n.png" alt="">
                  </div>
                </div>
              <div class="name-city">
                <div>{{wheater['tem_max']}}</div>
                <div>{{wheater['city'].name}}</div>
              </div>
              </div>
            <div class="indicators">
              <div>humedity {{wheater['humidity']}}</div>
              <div>west</div>
              <div>{{wheater['wind'].speed}}km/h</div>
            </div>
            </div>
          </div>
      </div>
    </div>
    <div class="elevate elevate-custom">
        <div class="container-input">
          <input placeholder="add location" v-on:keyup.enter="onEnter(city)" v-model="city" @blur="inactive"></input>
        </div>
        <div style="display: flex; justify-content:center">
            <img src="https://res.cloudinary.com/dutj1bbos/image/upload/c_scale,w_130/v1616196909/cherry-584_tmw938.png" alt="">
        </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      city: '',
      forecast: [],
      oneDay: []
    };
  },
  props: {
    image: {
      type: String,
      required: false
    },
    width: {
      type: [Number, String],
      default: "64"
    },
    height: {
      type: [Number, String],
      default: "64"
    },
    temperature: {
      type: String,
      default: "temperature"
    }
  },
  created() {
    // this.getData('lyon');
  },
  methods: {
    onEnter (city) {
      this.getData(this.city)
      this.filterDays()
    },
    inactive () {
      this.city = ''
    },
    getData(value) {
      var data = this;
      var xhr = new XMLHttpRequest();
      var url =
        `https://api.openweathermap.org/data/2.5/forecast?q=${value}&units=metric&mode=json&appid=${process.env.API.replace(/['"]+/g, '')}`;
      xhr.open("GET", url, false);
      xhr.onreadystatechange = function() {
        if (this.readyState === XMLHttpRequest.DONE) {
          if (this.status === 200) {
            data = this.responseText;
          } else {
            // console.log(this.status, this.statusText);
          }
        }
      };
      xhr.send();
      this.forecast = JSON.parse(data);
      // console.log(this.forecast)
    },
    filterDays() {
      const groupedData = this.forecast.list.reduce((days, row) => {
        const date = row.dt_txt.split(" ")[0];
        days[date] = [...(days[date] ? days[date] : []), row];
        return days;
      }, {});
      var i = 0;
      var y = 5;
      var data = []
      for (let date of Object.keys(groupedData)) {
        let wheater = groupedData[Object.keys(groupedData)[i]][i]["weather"][0];
        let date = Object.keys(groupedData)[i];
        let city = this.forecast.city
        let wind = this.forecast.list[0].wind
        i++;
        let arr = {
          tem_max: getMax(groupedData[date], "temp_max"),
          tem_min: getMin(groupedData[date], "temp_min"),
          humidity: getMax(groupedData[date], "humidity"),
          wheater,
          date,
          city,
          wind
        };
        data.push(arr);
        //  console.log(this.data);
      }
    this.oneDay.push(data[0])

      console.log(this.oneDay)
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
    },
  },
  computed: {
    size() {
      return {
        width: this.width + "px",
        height: this.height + "px"
      };
    }
  }
};
</script>

<style>
input {
  background: #EFEEFD;
  border: none;
  border-radius: 10px;
  padding: 5px;
  margin-top: 10px;
  margin-bottom: 60px;
  outline: none;
}
::-webkit-input-placeholder {
   text-align: center;

}
.container-input {
    display: flex;
    justify-content: center;
}
.location {
  width: 300px;
  height: 150px;
}
.icon-top {
  height: 100px;
  align-items: center;
}
</style>
