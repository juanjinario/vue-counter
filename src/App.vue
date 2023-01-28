<script setup>
import { computed, ref } from "vue";

const counter = ref(0);
const favoriteList = ref([]);

// Methods
const onDecrease = () => {
  counter.value--;
};
const onIncrease = () => {
  counter.value++;
};
const onReset = () => {
  counter.value = 0;
  favoriteList.value = [];
};
const onAddList = () => {
  favoriteList.value = [...favoriteList.value, counter.value];
};

// Computed
const classCounter = computed(() => {
  if (counter.value < 0) {
    return "c-red";
  } else if (counter.value === 0) {
    return "c-peru";
  } else {
    return "c-green";
  }
});
const existNumberInList = computed(() => {
  const existNumber = favoriteList.value.some(
    (number) => number === counter.value
  );
  if (existNumber) {
    return true;
  }
  return false;
});
</script>

<template>
  <header>
    <div class="logo-wrapper">
      <img
        alt="Vue logo"
        class="logo"
        src="./assets/logo.svg"
        width="125"
        height="125"
      />
    </div>
  </header>

  <main>
    <div>
      <button class="btn-accent" @click="onDecrease">- 1</button>
      <span class="main-counter-number" :class="classCounter">{{
        counter
      }}</span>
      <button class="btn-primary" @click="onIncrease">+ 1</button>
    </div>
    <div class="mt-4 d-flex gap-3">
      <button @click="onReset">Resetear</button>
      <button @click="onAddList" :disabled="existNumberInList">
        Añadir a 🧡
      </button>
    </div>

    <div class="fav-section">
      <h3>Lista de favoritos</h3>
      <ul v-if="favoriteList.length">
        <li
          class="opacity-75"
          v-for="(favNumber, index) of favoriteList"
          :key="index"
        >
          {{ favNumber }}
        </li>
      </ul>
      <span v-else class="opacity-50">
        Aun no se han añadido números a los favoritos
      </span>
    </div>
  </main>
</template>

<style scoped>
.c-peru {
  color: peru;
}
.c-red {
  color: red;
}

.c-green {
  color: green;
}
.logo-wrapper {
  margin-bottom: 4rem;
  text-align: center;
}
.main-counter-number {
  display: inline-block;
  font-size: 1.5rem;
  margin: auto 1rem;
  width: 3rem;
  text-align: center;
  transition: color 1s;
}

.fav-section {
  margin-top: 3rem;
}

.reset-row {
  margin-top: 1rem;
}

@media (min-width: 1024px) {
  .logo-wrapper {
    margin-bottom: 0;
  }
}
</style>
