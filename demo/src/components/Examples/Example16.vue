<template>
  <example-card
    link="https://github.com/setaman/vue-ellipse-progress/blob/demo/demo/src/components/Examples/Example13.vue"
  >
    <component
      :is="component"
      :progress="progress"
      :determinate="determinate"
      line="butt"
      :color="emptyColor"
      empty-color="#324c7e"
      :emptyColorFill="emptyColorFill"
      thickness="46"
      emptyThickness="8"
      :size="180"
      dash="strict 4 0.98"
      lineMode="in -8"
      legendClass="legend-custom-style"
      fontSize="1.5rem"
      font-color="white"
      animation="loop 500 100"
      :loading="loading"
      :no-data="noData"
    >
    </component>
  </example-card>
</template>

<script>
import ExampleCard from "@/components/Examples/ExampleCard";
import Interval from "@/utils/interval";
import props from "@/components/Examples/examplesProps";
import randomNumberInRange from "@/utils/randomNumberInRange";

export default {
  name: "Example16",
  components: { ExampleCard },
  props,
  data: () => ({
    progress: 0,
    sec: 0,
    min: 0,
    tasksDone: 125,
    emptyColor: {
      radial: true,
      colors: [
        {
          color: "#3260FC",
          offset: "50",
          opacity: "0.15",
        },
        {
          color: "#3260FC",
          offset: "70",
          opacity: "0.15",
        },
        {
          color: "#3260FC",
          offset: "70",
          opacity: "0.1",
        },
        {
          color: "#3260FC",
          offset: "90",
          opacity: "1",
        },
        {
          color: "#3260FC",
          offset: "60",
          opacity: "1",
        },
        {
          color: "#3260FC",
          offset: "0",
          opacity: "0",
        },
      ],
    },
    emptyColorFill: {
      radial: true,
      colors: [
        {
          color: "#3260FC",
          offset: "50",
          opacity: "0.2",
        },
        {
          color: "#3260FC",
          offset: "50",
          opacity: "0.15",
        },
        {
          color: "#3260FC",
          offset: "70",
          opacity: "0.15",
        },
        {
          color: "#3260FC",
          offset: "70",
          opacity: "0.1",
        },
        {
          color: "#3260FC",
          offset: "90",
          opacity: "0.1",
        },
        {
          color: "transparent",
          offset: "90",
          opacity: "0.1",
        },
        {
          color: "transparent",
          offset: "95",
          opacity: "0.1",
        },
        {
          color: "transparent",
          offset: "95",
          opacity: "0.1",
        },
      ],
    },
  }),
  computed: {
    component() {
      return this.test ? "vue-ellipse-progress-test" : "vue-ellipse-progress";
    },
  },
  methods: {
    randomizeProgress() {
      this.progress = randomNumberInRange(-50, 50);
    },
  },
  mounted() {
    Interval.addTask(this.randomizeProgress, 500);
  },
};
</script>

<style scoped></style>
