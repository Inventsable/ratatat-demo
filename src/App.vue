<template>
  <div id="app">
    <Panel>
      <Hello-World />
    </Panel>
  </div>
</template>

<script>
import starlette from "starlette";
export default {
  name: "App",
  components: {
    "Hello-World": require("@/components/HelloWorld.vue").default,
  },
  mounted() {
    starlette.initAs("ILST", "lightest");
  },
};
</script>

<style>
#app {
  font-size: 12px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.panel {
  font-size: 12px;
}
</style>
