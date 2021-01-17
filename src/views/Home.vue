<template>
  <div class="app-container">
    <div class="app-warpper">
      <div class="first-column">
        <input type="number" v-model="input" @change="enterNumber" />
      </div>
      <div class="second-column">
        <select v-model="modeSelected" @change="calculation">
          <option disabled value="">Please Select</option>
          <option>isPrime</option>
          <option>isFibonacci</option>
        </select>
      </div>
      <div class="third-column">{{ result }}</div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    input: 0,
    modeSelected: "",
    result: "NaN"
  }),
  methods: {
    enterNumber() {
      if (this.input < 0) {
        this.input = 1;
      }
      this.input = Math.round(this.input);
      this.calculation();
    },
    calculation() {
      if (this.modeSelected === "isPrime") {
        this.primeNumberCheck();
      } else if (this.modeSelected === "isFibonacci") {
        this.fibonacciNumberCheck();
      }
    },
    primeNumberCheck() {
      let isPrime = true;
      if (this.input <= 1) {
        isPrime = false;
      } else if (this.input > 1) {
        for (let i = 2; i < this.input; i++) {
          if (this.input % i == 0) {
            isPrime = false;
            break;
          }
        }
      }
      if (isPrime) {
        this.result = true;
      } else {
        this.result = false;
      }
    },
    fibonacciNumberCheck() {
      const fibonacci = (query, count = 1, last = 0) => {
        if (count < query) {
          return fibonacci(query, count + last, count);
        }
        if (count === query) {
          return true;
        }
        return false;
      };
      this.result = fibonacci(this.input);
    }
  }
};
</script>

<style lang="scss" scoped>
.app-container {
  height: 100vh;
  .app-warpper {
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: space-between;
    .first-column {
      width: 200px;
    }
    .second-column {
      flex: 1;
      border-right: 1px solid black;
      border-left: 1px solid black;
    }
    .third-column {
      width: 300px;
    }
  }
  @media only screen and (max-width: 600px) {
    .app-warpper {
      flex-direction: column;
      .second-column {
        border: none;
        flex: none;
      }
    }
  }
}
</style>
