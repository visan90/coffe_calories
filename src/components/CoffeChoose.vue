<template>
  <div>
    <img class="calculator__img" :src="filteredImage.link" :alt="filteredImage.name">
    <p class="calculator__total-calories">Total calories {{totalCalories}}</p>
    <ul class="calculator__wrap">
      <li class="calculator__item">
        <label class="calculator__description" for="coffee_type">Coffee Type</label>
        <select
          v-model="coffeeType"
          @change="getCoffeeType($event)"
          id="coffee_type"
          class="calculator__select"
          >
          <option v-for="item in coffee" :value="item.name" :key="item.name">{{item.name}}</option>
        </select>
      </li>
      <li class="calculator__item">
        <label class="calculator__description" for="cup_size">Cup Size</label>
        <select
          v-model="coffeeCalories"
          id="cup_size"
          class="calculator__select"
          >
          <option
            v-for="item in filteredList"
            :value="item.caloriesSmall"
            :key="item.caloriesSmall"
          >Small cup</option>
          <option
            v-for="item in filteredList"
            :value="item.caloriesLarge"
            :key="item.caloriesLarge"
          >Large cup</option>
        </select>
      </li>
      <li class="calculator__item">
        <label class="calculator__description" for="cream">Cream</label>
        <select
          v-model="coffeeCream"
          id="cream"
          class="calculator__select"
          >
          <option v-for="item in cream" :value="item">{{item}}</option>
        </select>
      </li>
      <li class="calculator__item">
        <label class="calculator__description" for="sugar">tbsp of Sugar</label>
        <select
          v-model="coffeeSugar"
          id="sugar"
          class="calculator__select"
          >
          <option
            v-for="item in sugar"
            :value="item.calories"
            :key="item.qty"
            >
            {{item.qty}}
          </option>
        </select>
      </li>
    </ul>
    <p
      v-if="randomNumber == 1"
    >You need to walk for {{caloriesBurnWalking}} minutes at a normal pace to burn that amount of calories.</p>
    <p
      v-if="randomNumber == 2"
    >You need to run for {{caloriesBurnRunning}} minutes at a rate of 9.6 km/hour to burn that amount of calories.</p>
    <p
      v-if="randomNumber == 3"
    >You need to cycle for {{caloriesBurnCycling}} minutes at a rate of 21 km/hour to burn that amount of calories.</p>
  </div>
</template>

<script>
export default {
  name: "CoffeChoose",
  props: ["item"],
  components: {},
  data: function() {
    return {
      coffeeCalories: 60,
      message: "",
      coffeeCream: "no",
      coffeeType: "Cappuccino",
      coffeeSugar: 0,
      randomNumber: "",
      coffee: [
        {
          name: "Cappuccino",
          caloriesSmall: 60,
          caloriesLarge: 90,
          link: "images/Cappuccino.jpg"
        },
        {
          name: "Cafe Latte",
          caloriesSmall: 95,
          caloriesLarge: 142,
          link: "images/CafeLatte.jpg"
        },
        {
          name: "Cafe Mocha",
          caloriesSmall: 210,
          caloriesLarge: 360,
          link: "images/CafeMocha.jpg"
        },
        {
          name: "Cafe Au Lait",
          caloriesSmall: 75,
          caloriesLarge: 113,
          link: "images/CafeAuLait.jpg"
        },
        {
          name: "Irish Coffee",
          caloriesSmall: 228,
          caloriesLarge: 456,
          link: "images/IrishCoffee.jpg"
        },
        {
          name: "Cafe Americano",
          caloriesSmall: 5,
          caloriesLarge: 7,
          link: "images/CafeAmericano.jpg"
        },
        {
          name: "Espresso",
          caloriesSmall: 3,
          caloriesLarge: 6,
          link: "images/Espresso.jpg"
        },
        {
          name: "Frappe",
          caloriesSmall: 204,
          caloriesLarge: 408,
          link: "images/Frappe.jpg"
        }
      ],
      cream: ["yes", "no"],
      sugar: [
        {
          qty: "none",
          calories: 0
        },
        {
          qty: "1 tbsp",
          calories: 55
        },
        {
          qty: "2 tbsp",
          calories: 110
        },
        {
          qty: "3 tbsp",
          calories: 165
        }
      ],
      creamCalories: 33
    };
  },
  methods: {
    getCoffeeType(event) {
      this.coffeeCalories = this.coffee.find(item => {
        return item.name.includes(event.target.value);
      }).caloriesSmall;
    }
  },
  computed: {
    filteredList() {
      return this.coffee.filter(item => {
        return item.name.includes(this.coffeeType);
      });
    },
    totalCalories() {
      if (this.coffeeCream == "yes") {
        return this.coffeeCalories + this.creamCalories + this.coffeeSugar;
      } else {
        return this.coffeeCalories + this.coffeeSugar;
      }
    },
    filteredImage() {
      return this.coffee.find(item => {
        return item.name.includes(this.coffeeType);
      });
    },
    caloriesBurnRunning() {
      return Math.ceil(this.totalCalories / 12.3);
    },
    caloriesBurnWalking() {
      return Math.ceil(this.totalCalories / 4.16);
    },
    caloriesBurnCycling() {
      return Math.ceil(this.totalCalories / 11.53);
    }
  },
  watch: {
    totalCalories: function() {
      var storeRandomNumber = Math.floor(Math.random() * 3) + 1;
      this.randomNumber = storeRandomNumber;
    }
  }
};
</script>

<style lang="scss" scoped>
h3 {
  margin: 40px 0 0;
}
.calculator__total-calories {
  font-weight: 700;
  font-size: 18px;
}
.calculator__wrap {
  list-style-type: none;
  padding: 0;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}
.calculator__item {
  display: inline-block;
  margin: 0 10px;
  display: flex;
  flex-direction: column;
}
.calculator__description {
  padding: 10px 0;
}
.calculator__select {
  padding: 5px;
}
a {
  color: #42b983;
}

.calculator__img {
  width: 400px;
  height: 300px;
  box-shadow: 0px 16px 18px -8px rgba(161,161,161,1);
}
</style>
