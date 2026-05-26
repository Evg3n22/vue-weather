<script setup></script>

<template>
  <div class="weather">
    <div class="container">

      <div class="card weather-form">
        <input type="text" placeholder="Enter city name" 
        class="weather-input__form">
        <button class="weather-form__btn">Search</button>
      </div>

      <div class="card weather-load">Loading...</div>

      <div class="weather-info">
        <div class="weather-info__text">
          <p class="card">Phuket</p>
          <p class="card">29 C</p>
          <p class="card">Sunny</p>
        </div>
      </div>

    </div>
    

    <div class="weather-bg">
      <div>
        <img class="weather-bg__img bg" src="./assets/bg.jpg" alt="bg">
        <img class="weather-bg sunny" src="./assets/sunny.jpg" alt="sunny">
        <img class="weather-bg rainy" src="./assets/rainy.jpg" alt="rainy">
        <img class="weather-bg cloudy" src="./assets/cloudy.jpg" alt="cloudy">
      </div>
    </div>
  </div>
</template>
