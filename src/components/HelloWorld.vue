<template>
  <div class="master-wrapper">
    <Wrapper>
      <Grid>
        <Dropdown
          label="Current easing"
          :items="items"
          :active="0"
          @update="updateActiveEaser"
        />
        <Dropdown
          label="Easing Type"
          :items="types"
          :active="0"
          @update="updateActiveType"
        />
      </Grid>

      <Grid>
        <Drumroll
          layer="controller"
          slider="test"
          :animation-data="eyeAnim"
          :percent="currentVal"
          :timing="currentTiming"
          :duration="duration"
        />
        <Drumroll
          layer="controller"
          slider="test"
          :animation-data="circAnim"
          :percent="currentVal"
          :timing="currentTiming"
          :duration="duration"
        />
        <Drumroll
          layer="MASTER"
          slider="CONTROL"
          :animation-data="wingAnim"
          :percent="currentVal"
          :timing="currentTiming"
          :duration="duration"
          @start="startMsg"
          @end="endMsg"
          @update="updateScore"
        />
      </Grid>

      <Divider dark />
      <Anno size="42px">{{ `value is ${score}` }}</Anno>
      <Grid>
        <Input-Scroll
          label="Duration"
          :min="0"
          :max="2000"
          :value="duration"
          @update="(val) => (duration = val)"
        />
        <Input-Scroll
          ref="updateTime"
          label="Change percent"
          :min="0"
          :max="100"
          :value="0"
          @update="updateAll"
        />
        <Input-Scroll
          ref="realTime"
          label="Realtime"
          :min="0"
          :max="100"
          :value="0"
          @change="updateAll"
        />
      </Grid>

      <Anno size="20px">Use the sliders above to change the value of each</Anno>
    </Wrapper>
  </div>
</template>

<script>
export default {
  mounted() {},
  components: {
    Drumroll: require("ratatat").default,
  },
  data: () => ({
    currentVal: 0,
    duration: 600,
    score: 0,
    items: [
      "quad",
      "quart",
      "quint",
      "cubic",
      "expo",
      "sine",
      "circ",
      "back",
      "elastic",
      "bounce",
    ],
    types: ["in", "out", "in-out"],
    activeType: "",
    activeEase: "",
    eyeAnim: require("./eye.json"),
    circAnim: require("./circle.json"),
    wingAnim: require("./wings.json"),
  }),
  computed: {
    currentTiming() {
      return `${this.activeType}-${this.activeEase}`;
    },
  },
  methods: {
    updateAll(value) {
      this.currentVal = value;
      if (this.$refs.updateTime.val !== value)
        this.$refs.updateTime.val = value;
      if (this.$refs.realTime.val !== value) this.$refs.realTime.val = value;
    },
    updateActiveEaser(value) {
      this.activeEase = value;
    },
    updateActiveType(value) {
      this.activeType = value;
    },
    startMsg() {
      console.log("START");
    },
    endMsg() {
      console.log("END");
    },
    updateScore(val) {
      // console.log(val);
      this.score = `${val}%`;
    },
  },
};
</script>

<style>
.master-wrapper {
  width: 800px;
}
.anim-main {
  fill: var(--color-selection);
  stroke: var(--color-selection);
}

.anim-dark {
  fill: rgba(0, 0, 0, 0.2);
}
.anim-dark-str1 {
  stroke: rgba(0, 0, 0, 0.2);
}
.anim-dark-str {
  stroke: transparent;
}

.anim-mask {
  fill: transparent;
}

.anim-bg {
  fill: var(--color-bg);
  stroke: var(--color-bg);
}
</style>
