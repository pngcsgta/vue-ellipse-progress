<template>
  <example-card
    link="https://github.com/setaman/vue-ellipse-progress/blob/demo/demo/src/components/Examples/Example17.vue"
  >
    <component
      class="example-circle"
      :is="component"
      :progress="progress"
      :determinate="determinate"
      :loading="loading"
      :no-data="noData"
      color="#7579ff"
      empty-color="#324c7e"
      :size="180"
      :thickness="5"
      :empty-thickness="3"
      :legend-value="price"
      animation="rs 3000"
    >
      <template v-slot:default="{ counterTick: { currentValue } }">
        <div class="price" :style="{ color: determineColor(currentValue) }">
          <img width="25" :src="require('@/assets/euro.svg')" />
          <span>
            {{
              new Intl.NumberFormat("de-DE", { style: "currency", currency: "EUR" })
                .format(currentValue)
                .replace("€", "")
                .trim()
            }}
          </span>
        </div>
        <!--<span>€</span>-->
      </template>
    </component>
  </example-card>
</template>

<script>
import ExampleCard from "@/components/Examples/ExampleCard";
import Interval from "@/utils/interval";
import randomNumberInRange from "@/utils/randomNumberInRange";
import props from "@/components/Examples/examplesProps";

export default {
  name: "Example17",
  components: { ExampleCard },
  props,
  data: () => ({
    progress: 0,
    price: 0,
    priceColor: "red",
    colorSteps: {
      0: "RED",
      1: "LIGHTCORAL",
      2: "DARKORANGE",
      3: "PALEGOLDENROD",
      4: "SPRINGGREEN",
    },
  }),
  computed: {
    component() {
      return this.test ? "vue-ellipse-progress-test" : "vue-ellipse-progress";
    },
  },
  methods: {
    determineColor(value) {
      const progress = (value * 100) / 1000;
      let index = 0;
      for (const step of [20, 40, 60, 80, 100]) {
        if (progress > step) {
          index += 1;
        } else {
          return this.colorSteps[index];
        }
      }
    },
    randomizeOptions() {
      this.price = randomNumberInRange(-1000, 1000, false);
      this.progress = (this.price * 100) / 1000;
    },
  },
  mounted() {
    Interval.addTask(this.randomizeOptions, 3000);
  },
};
</script>

<style scoped lang="scss">
.price {
  display: flex;
  transition: 3s;
  font-size: 1.8rem;
  font-weight: bold;
  color: red;
  img {
    position: relative;
    top: -3px;
  }
}
</style>
