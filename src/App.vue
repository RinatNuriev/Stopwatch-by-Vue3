<template>
  <div class="container">
    <div class="boxes">
      <div v-for="(child, index) in children" :key="index">
        <component :is="child"></component>
      </div>
      <div class="addStopwatch" @click="addStopwatch">
        <div class="plus alt">
        </div>
      </div>
    </div>

  </div>
</template>

<script>
import Stopwatch from './components/Stopwatch.vue';

export default {
  components: {
    Stopwatch
  },
  data() {
    return {
      children: [Stopwatch],
      counter: 0,
    }
  },
  methods: {
    addStopwatch() {
      this.counter++;
      this.children.push(Stopwatch);

    }
  }
}
</script>

<style scoped>
.addStopwatch {
  width: 225px;
  height: 120px;
  background: #696969;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  transition: all .2s ease;
}

.addStopwatch:hover {
  background: #E5E5E5;
}

.plus {
  display: inline-block;
  width: 50px;
  height: 50px;
  background:
    linear-gradient(#fff, #fff),
    linear-gradient(#fff, #fff),
    #000;
  background-position: center;
  background-size: 50% 2px, 2px 50%;
  background-repeat: no-repeat;
}

.alt {
  background:
    linear-gradient(#9E9E9E, #9E9E9E),
    linear-gradient(#9E9E9E, #9E9E9E);
  background-position: center;
  background-size: 50% 2px, 2px 50%;
  background-repeat: no-repeat;
}
</style>

