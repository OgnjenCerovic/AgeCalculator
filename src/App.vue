<template>
  <div class="container">
    <h1>Age Calculator</h1>
    <div class="input-form">
      <form @submit.prevent="calculateAge">
        <InputForm label="Day" type="number" v-model="day" />
        <InputForm label="Month" type="number" v-model="month" />
        <InputForm label="Year" type="number" v-model="year" />
        <button type="submit" class="form-button">Calculate Age</button>
      </form>
    </div>
    <CalculationResult :age="age" />
  </div>
</template>

<script>
import InputForm from './components/InputForm.vue';
import CalculationResult from './components/CalculationResult.vue';

export default {
  components: {
    InputForm,
    CalculationResult
  },
  data() {
    return {
      day: '',
      month: '',
      year: '',
      age: null
    };
  },
  methods: {
    calculateAge() {

      const today = new Date();

      if (this.year > today.getFullYear()) {
        alert("Birth year cannot be in the future");
        this.age = null;
        return;
      }
      const birthdate = new Date(this.year, this.month - 1, this.day);
      let years = today.getFullYear() - birthdate.getFullYear();
      let months = today.getMonth() - birthdate.getMonth();
      let days = today.getDate() - birthdate.getDate();

      if(months > 12){
        alert("Month should not be greater then 12");
        this.age = null;
        return;
      }

      if (days < 0) {
        months -= 1;
        days += new Date(today.getFullYear(), today.getMonth(), 0).getDate();
      }

      if (months < 0) {
        years -= 1;
        months += 12;
      }

      this.age = { years, months, days };
    }
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Ubuntu+Sans:ital,wght@0,100..800;1,100..800&display=swap');

.container {
  background-color: rgb(241, 240, 240);
  font-family: "Ubuntu Sans", sans-serif;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  font-size: 20px;
  height: 400px;
  padding: 200px;
}

.container h1 {
  text-align: center;
}

.input-form {
  display: flex;
  align-items: center;
  width: 500px;
  justify-content: center;
}

.form-group {
  display: flex;
  flex-direction: column;
  font-size: 20px;
}

.form-group input {
  font-size: 20px !important;
}

.form-button {
  width: 100%;
  margin-top: 20px;
  color: white;
  border: none;
  background-color: #008a4f;
  padding: 10px 0;
  cursor: pointer;
  transition: all .2s ease-in;
  font-family: "Ubuntu Sans", sans-serif;
  font-size: 20px;
}

.form-button:hover {
  opacity: 0.8;
  transform: scale(1.07);
}
</style>
