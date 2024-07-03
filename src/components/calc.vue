<template>
  <a target="_blank" href="https://mgavm.ru/abitur/"><img class="logo" src="../assets/logo.svg" alt=""></a>
  <section class="calculator-section">
    <h1 class="calculator-h1">Калькулятор <span class="calculator-h1__span">среднего балла</span></h1>
    <p class="calculator-description">Рассчитайте средний балл для диплома или аттестата с помощью онлайн-калькулятора</p>
    <article class="calc-block">
      <div class="calculator">
        <div class="calc-input__block">
          <h3 class="calc-input__block">Отлично (кол-во 5)</h3>
          <input type="number" v-model="five" class="calc-input five">
        </div>
        <div class="calc-input__block">
          <h3 class="calc-input__block">Хорошо (кол-во 4)</h3>
          <input type="number" v-model="fourth" class="calc-input fourth">
        </div>
        <div class="calc-input__block">
          <h3 class="calc-input__block">Удовл. (кол-во 3)</h3>
          <input type="number" v-model="three" class="calc-input three">
        </div>
        <div class="calc-input__block">
          <h3 class="calc-input__block">Неуд. (кол-во 2)</h3>
          <input type="number" v-model="two" class="calc-input two">
        </div>
      </div>
      <div class="calc-res">
        <h2 class="calc-res__middle">Средний балл равен:</h2>
        <div class="calc-res__resNum">{{ res }}</div>
      </div>
    </article>
  </section>
</template>

<script>
import { ref, computed } from 'vue';

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  setup() {
    const five = ref(0);
    const fourth = ref(0);
    const three = ref(0);
    const two = ref(0);


    const fivesum = computed(() => five.value * 5);
    const fourthsum = computed(() => fourth.value * 4);
    const threesum = computed(() => three.value * 3);
    const twosum = computed(() => two.value * 2);

    const sum = computed(() => fivesum.value + fourthsum.value + threesum.value + twosum.value);

    const allnums = computed(() => +five.value + +fourth.value + +three.value + +two.value);

    const calc = computed(() => {
      let res = sum.value / allnums.value;
      return isNaN(res) ? '0' : res.toFixed(2);
    });

    return {
      five,
      fourth,
      three,
      two,
      res: calc
    };
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}

.logo {
  max-width: 200px;
  margin-right: auto;
}
.calculator-section {
  margin-top: 100px;
  display: flex;
  flex-direction: column;
  gap: 30px;
  width: 100%;
  align-items: center;
}

.calculator-h1 {
  font-size: 3.5rem;
  font-weight: 800;
}

.calculator-h1__span {
  background-image: linear-gradient(47deg, rgba(24, 22, 196, 1) 0%, rgba(0, 168, 255, 1) 100%);
  ;
  color: transparent;
  -webkit-background-clip: text;
  background-clip: text;
  font-weight: 800;
}

.calculator-description {
  width: 40%;
  text-align: center;
  font-size: 1.5rem;
}

.calc-block {
  display: flex;
  flex-direction: row;
  gap: 50px;
  margin-top: 100px;
  flex-wrap: wrap;
}

.calculator {
  width: 50%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 40px;
  align-items: center;
  justify-content: center;
}

.calc-res {
  display: flex;
  flex-direction: column;
  gap: 30px;
  align-items: center;
  width: 30%;
  padding: 30px;
  background-color: #f7f6f6;
  border-radius: 50px;
}

.calc-input {
  position: relative;
  border: none;
  border-radius: 10px;
  max-width: 250px;
  outline: none;
  border-bottom: 1px solid #516bff;
  padding: 10px;
  font-size: 2rem;
  -webkit-box-shadow: 0px 0px 8px 2px rgba(34, 60, 80, 0.2);
  -moz-box-shadow: 0px 0px 8px 2px rgba(34, 60, 80, 0.2);
  box-shadow: 0px 0px 8px 2px rgba(34, 60, 80, 0.2);
}


.calc-input::-webkit-outer-spin-button,
.calc-input::-webkit-inner-spin-button {
  /* display: none; <- Crashes Chrome on hover */
  -webkit-appearance: none;
  margin: 0;
  /* <-- Apparently some margin are still there even though it's hidden */
}


.calc-input:focus {
  outline: #516bff;
  border: 1px solid #516bff;
}

.calc-input__block {
  font-weight: 400;
  font-size: 0.9rem;
  color: rgb(133, 133, 133);
}

.calc-res__middle {
  font-size: 2rem;
  font-weight: 500;
}

.calc-res__resNum {
  font-size: 5rem;
  font-weight: bold;
  background-image: linear-gradient(47deg, rgba(24, 22, 196, 1) 0%, rgba(0, 168, 255, 1) 100%);
  ;
  color: transparent;
  -webkit-background-clip: text;
  background-clip: text;
  transition: 0.3;
}

.calc-input__block {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

@media screen and (max-width: 620px) {
  .calculator-h1 {
    font-size: 2.5rem;
  }

  .calculator-description {
    font-size: 1rem;
    width: 80%;
  }
  
  .calc-block {
    margin-top: 40px;
  }

  .calculator {
    width: 100%;
  }

  .calc-res {
    width: 100%;
  }

}

</style>
