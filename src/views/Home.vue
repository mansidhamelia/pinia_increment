<template>
  <div class="home">
    <p>Double count is {{ store.doubleCount }}</p>
    <p>Double plus one count is {{ store.doublePlusOne }}</p>

    <h4>{{ counter }}</h4>
    <button @click="increment">Click me</button>
    <button @click="reset">reset</button>

    <button @click="$router.push('/event')">Form</button>

    <!-- <p> user 2: {{ getUserById(2)}}</p> -->
  </div>
</template>

<script>
// @ is an alias to /src
import { useStore } from "../store/counter";
import { storeToRefs, mapActions } from "pinia";
import { computed } from "vue";
import { useRouter } from "vue-router";

export default {
  setup() {
    const store = useStore();
    const router = useRouter();
    const { counter } = storeToRefs(store);

    // store.randomizeCounter();

    // another way for double value using computed
    // const {double} = computed((store) => store.counter * 2);
    const { increment } = store;

    // one way
    function add(number) {
      store.$patch({
        counter: counter.value + number,
      });
    }
    // another way
    function addOne(number) {
      store.$patch((state) => (state.counter += number));
    }
    function reset() {
      store.$reset();
    }
    function goTo() {}
    return {
      store,
      counter,
      increment,
      add,
      addOne,
      reset,
      // getUserById: store.getUserById,
    };
  },
};
</script>
