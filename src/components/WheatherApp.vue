<template>
<!-- eslint-disable -->
  <div class="container">
    <div class="app__content" :class="{ app__content_blue: isCold }">
      <div class="app__search">
        <input type="text" class="app__searchfield fieldsearch"
               v-model="query"
               @keypress="fetchWeather"
               placeholder="Search Location...">
      </div>
      <transition name="fade">
      <div class="app__body body" v-if="typeof weather.main != 'undefined'">
        <h2 class="body__city">
          {{ weather.name || 'Select city' }}, {{ weather.sys.country }}
        </h2>
        <p class="body__today">
          {{ today }}
        </p>
        <p class="body__temperature">
          {{ (Math.round(weather.main.temp) || '0') + '°C' }}
        </p>
        <p class="body__separator">
          ----------
        </p>
        <p class="body__description">
          {{ weather.weather[0].description }}
        </p>
        <p class="body__temperatureAll">
          {{ (Math.round(weather.main.temp_max) || '0') + '°C' }}/ {{ (Math.round(weather.main.temp_min) || '0') + '°C' }}
        </p>
      </div>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      WeatherAPI: 'b2bfd67809b854f6308d532784e14bbb',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {},
      today: this.getNameDay(),
      isCold: false,
    };
  },
  watch: {
    // eslint-disable-next-line
    query: function(newValue) {
      // eslint-disable-next-line
      gsap.to(this.$data, { duration: 0.2, weather: newValue });
    },
  },
  methods: {
    fetchWeather(e) {
      if (e.key === 'Enter') {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.WeatherAPI}`)
        // eslint-disable-next-line
          .then(res => {
            return res.json();
          }).then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
      this.checkCold();
    },
    getNameDay() {
      const days = [
        'Sunday',
        'Monday',
        'Tuesday',
        'Wednesday',
        'Thursday',
        'Friday',
        'Saturday',
      ];
      const date = new Date();
      const number = date.getDay();
      return `${days[number]}`;
    },
    checkCold() {
      if (Math.round(this.weather.main.temp) < 20) {
        this.isCold = true;
      } else {
        this.isCold = false;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.container {
  width: 405px;
  margin: 25px auto 0 auto;
  padding: 0 15px
}
.app {
  &__content {
    width: 432px;
    height: 768px;
    filter: drop-shadow(3px 3px 20px rgba(0, 0, 0, 0.35));
    border-radius: 20px;
    background-image: url(./../static/bg_red.png);
    display: flex;
    flex-direction: column;
    justify-content: start;
  }
  &__content_blue {
    background-image: url(./../static/bg_blue.png);
  }
  &__search {
    display: flex;
    justify-content: center;
    align-items: center;
    justify-self: start;
    margin-top: 25px;
  }
  &__searchfield {
  }
  &__body {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    transition: 0.4s;
  }
}
.body {
  &__city {
    font-weight: 500;
    font-size: 50px;
    // line-height: 59px;
    text-align: center;
    color: #000000;
    margin-top: 85px;
  }
  &__today {
    font-size: 25px;
    // line-height: 30px;
    text-align: center;
    color: #000000;
  }
  &__temperature {
    font-weight: 700;
    font-size: 75px;
    // line-height: 89px;
    text-align: center;
    color: #000000;
  }
  &__separator {
    font-size: 50px;
    // line-height: 59px;
    text-align: center;
    color: #000000;
  }
  &__description {
    font-weight: 500;
    font-size: 25px;
    // line-height: 30px;
    text-align: center;
    color: #FFFFFF;
  }
  &__temperatureAll {
    font-weight: 500;
    font-size: 25px;
    // line-height: 30px;
    text-align: center;
    color: #FFFFFF;
  }
}
.fieldsearch {
  width: 375px;
  height: 43px;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  font-family: 'Rubik';
  font-style: normal;
  font-weight: 400;
  font-size: 17px;
  // line-height: 20px;
  color: #313131;
  padding-left: 16px;
  transition: 0.4s;
}
.fieldsearch:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
