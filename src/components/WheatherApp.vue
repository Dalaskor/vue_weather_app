<template>
<!-- eslint-disable -->
  <div class="container">
    <div class="app__content">
      <div class="app__search">
        <input type="text" class="app__searchfield fieldsearch" v-model="cityName"
               placeholder="Search Location...">
      </div>
      <div class="app__body body">
        <h2 class="body__city">
          {{ cityName }}
        </h2>
        <p class="body__today">
          {{ today }}
        </p>
        <p class="body__temperature">
          {{ (temperature || '0') + '°C' }}
        </p>
        <p class="body__separator">
          ----------
        </p>
        <p class="body__description">
          {{ wheatherDescription }}
        </p>
        <p class="body__temperatureAll">
          {{ (temperatureAll || '0/ 0') + '°C'  }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cityName: 'cityName',
      today: 'Monday',
      temperature: '16',
      wheatherDescription: 'Broken Clouds',
      temperatureAll: '17/ 9',
    };
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
    justify-content: center;
  }
  &__search {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  &__searchfield {
  }
  &__body {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
}
.body {
  &__city {
    font-weight: 500;
    font-size: 50px;
    // line-height: 59px;
    text-align: center;
    color: #000000;
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
  background: #FFFFFF;
  box-shadow: 3px 4px 20px rgba(0, 0, 0, 0.25);
  border-radius: 0px 10px;
  font-family: 'Rubik';
  font-style: normal;
  font-weight: 400;
  font-size: 17px;
  // line-height: 20px;
  color: #7E7E7E;
  padding-left: 16px;
}
</style>
