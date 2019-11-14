<template>
  <div id="app">
    <div class="mainBox">
      <HelloWorld />
      <Tip />
      <Btn />
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld";
import Tip from "./components/Tip";
import Btn from "./components/Btn";

export default {
  name: "app",
  components: {
    HelloWorld,
    Btn,
    Tip
  }
};
</script>
<style scoped>
.mainBox {
  background: #fff;
   
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
}
</style>
