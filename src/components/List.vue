<template>
  <div class="list">
    <h2>List</h2>
    <ul class="list-timers">
      <li v-for="timer in timers" :key="timer">
        <Timer />
      </li>
    </ul>
    <button class="add-timer" @click="addTimer">&#43;</button>
  </div>
</template>

<script>
import { ref } from "vue";
import Timer from "./Timer.vue";

export default {
  name: "List",
  components: {
    Timer,
  },
  setup() {
    const timers = ref(2);

    const addTimer = () => {
      timers.value++;
    };

    return {
      timers,
      addTimer,
    };
  },
};
</script>

<style lang="scss">
.list {
  display: flex;
  flex-direction: column;
  align-items: center;
  flex: 1 1 auto;
  padding: 20px;

  &-timers {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;

    li {
      max-width: 300px;
      width: 100%;
    }
  }
}
.add-timer {
  max-width: 300px;
  width: 100%;
  height: 100px;
  color: #d5d5d5;
  font-size: 40px;
  text-align: center;
  background-color: #a8a8a8;
  border: none;
}
</style>
