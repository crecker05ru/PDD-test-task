<template>
  <div :class="{ timer: true, stopped: isStoped }">
    <div class="time">{{ timeStamp }}</div>
    <div class="timer-buttons">
      <button
        :class="{ 'button-play': !isRuning, 'button-pause': isRuning }"
        @click="startTime"
      ></button>
      <button class="button-stop" @click="stopTime"></button>
    </div>
  </div>
</template>

<script>
import { computed, ref } from "vue";
export default {
  name: "Timer",
  setup() {
    let time = ref(0);
    let millisec = ref(0);
    let sec = ref(0);
    let min = ref(0);
    let hour = ref(0);
    let isRuning = ref(false);
    let isStoped = ref(false);

    let milliseconds = computed(() => {
      time.value % 1 === 0 && time.value > 0 ? (millisec.value += 1) : millisec.value;
      millisec.value % 100 === 0 ? (millisec.value = 0) : 0;
      return millisec.value;
    });

    let seconds = computed(() => {
      millisec.value >= 99 && millisec.value > 0 ? (sec.value += 1) : sec.value;
      sec.value > 59 ? (sec.value = 0) : 0;
      return sec.value;
    });

    let minutes = computed(() => {
      time.value % (100 * 60) === 0 && time.value > 0 ? (min.value += 1) : min.value;
      min.value > 59 ? (min.value = 0) : 0;
      return min.value;
    });

    let hours = computed(() => {
      time.value % (100 * 60 * 60) === 0 && time.value > 0
        ? (hour.value += 1)
        : hour.value;
      hour.value > 23 ? "a day later" : 0;
      return hour.value;
    });

    let timeStamp = computed(() => {
      return `${hours.value}:${String(minutes.value).padStart(2, "0")}:${String(
        seconds.value
      ).padStart(2, "0")}:${String(milliseconds.value).padStart(2, "0")}`;
    });

    let timId;

    const startTime = () => {
      console.log("isRuning.value", isRuning.value);
      if (!isRuning.value) {
        timId = setInterval(() => (time.value += 1), 10);
        isRuning.value = true;
      } else {
        console.log("clearInterval(timId)");
        clearInterval(timId);
        isRuning.value = false;
      }
    };
    const stopTime = () => {
      clearInterval(timId);
      isStoped.value = true;
    };

    return {
      timeStamp,
      isRuning,
      isStoped,
      startTime,
      stopTime,
    };
  },
};
</script>

<style lang="scss">
.timer {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-around;
  background-color: #a8a8a8;
  font-size: 20px;
  margin-bottom: 40px;

  &-buttons {
    padding: 10px;
    position: relative;

    button {
      width: 20px;
      height: 20px;
      text-align: center;
      position: relative;
    }
  }
}

.time {
  width: 100%;
  padding: 10px;
  color: #fff;
  text-align: center;
  border-bottom: 1px solid #fff;
}

.stopped {
  opacity: 0.5;
  pointer-events: none;
}

.button {
  &-play {
    margin-right: 20px;
    background: linear-gradient(#d5d5d5, #d5d5d5);
    clip-path: polygon(0% 100%, 50% 0%, 100% 100%);
    transform: rotate(90deg);
    border-top: 5px solid transparent;
    border-bottom: 5px solid transparent;
  }

  &-pause {
    margin-right: 20px;
    background-color: transparent;
    transform: rotate(90deg);
    border-top: 5px solid #d5d5d5;
    border-bottom: 5px solid #d5d5d5;
  }

  &-stop {
    background-color: #d5d5d5;
    border-top: 5px solid transparent;
    border-bottom: 5px solid transparent;
  }
}
</style>
