<script setup lang="ts">
const countOne = ref(0);
const countTwo = ref(0);
const countThree = ref(0);
const countFour = ref(0);

const resetAll = () => {
  countOne.value = 0;
  countTwo.value = 0;
  countThree.value = 0;
  countFour.value = 0;
};

const areMultipleClicked = computed(() =>
  Boolean(
    [countOne.value, countTwo.value, countThree.value, countFour.value].filter(
      (v) => v
    ).length > 1
  )
);

const LS_KEY = "triangle-data";

const saveToLS = () => {
  localStorage.setItem(
    LS_KEY,
    JSON.stringify([
      countOne.value,
      countTwo.value,
      countThree.value,
      countFour.value,
    ])
  );
};

onMounted(() => {
  const parsedDataFromLS: number[] = JSON.parse(
    localStorage.getItem(LS_KEY) ?? "[0,0,0,0]"
  );

  countOne.value = parsedDataFromLS[0];
  countTwo.value = parsedDataFromLS[1];
  countThree.value = parsedDataFromLS[2];
  countFour.value = parsedDataFromLS[3];
});

watch([countOne, countTwo, countThree, countFour], saveToLS);
</script>

<template>
  <div class="min-h-screen py-6 bg-gray-900">
    <div
      class="flex flex-col items-center gap-24 py-6 overflow-hidden size-full"
    >
      <div class="flex flex-wrap rotate-45 size-64 lg:size-96">
        <div class="relative overflow-hidden size-1/2">
          <button
            @click="countOne++"
            type="button"
            class="relative transition-opacity duration-300 origin-center scale-150 rotate-45 translate-x-1/2 translate-y-1/2 bg-white touch-manipulation top-3 size-full transform-gpu hover:opacity-70"
          ></button>
          <div
            v-if="countOne"
            class="absolute -rotate-45 -translate-x-1/2 -translate-y-1/2 top-1/2 left-1/2"
          >
            <div
              class="absolute -translate-x-1/2 -translate-y-2 bottom-full left-1/2"
            >
              <base-button text="reset" @click="countOne = 0" />
            </div>
            <p class="p-2 text-xl font-bold pointer-events-none bg-slate-200">
              {{ countOne }}
            </p>
          </div>
        </div>
        <div class="relative overflow-hidden size-1/2">
          <button
            @click="countTwo++"
            type="button"
            class="relative transition-opacity duration-300 origin-center scale-150 rotate-45 -translate-x-1/2 translate-y-1/2 bg-red-500 touch-manipulation top-3 size-full transform-gpu hover:opacity-70"
          ></button>
          <div
            v-if="countTwo"
            class="absolute -rotate-45 -translate-x-1/2 -translate-y-1/2 top-1/2 left-1/2"
          >
            <div
              class="absolute translate-x-2 -translate-y-1/2 left-full top-1/2"
            >
              <base-button text="reset" @click="countTwo = 0" />
            </div>

            <p class="p-2 text-xl font-bold pointer-events-none bg-slate-200">
              {{ countTwo }}
            </p>
          </div>
        </div>
        <div class="relative overflow-hidden size-1/2">
          <button
            @click="countThree++"
            type="button"
            class="relative transition-opacity duration-300 origin-center scale-150 rotate-45 translate-x-1/2 -translate-y-1/2 bg-blue-500 touch-manipulation -top-3 size-full transform-gpu hover:opacity-70"
          ></button>
          <div
            v-if="countThree"
            class="absolute -rotate-45 -translate-x-1/2 -translate-y-1/2 top-1/2 left-1/2"
          >
            <div
              class="absolute -translate-x-2 -translate-y-1/2 right-full top-1/2"
            >
              <base-button text="reset" @click="countThree = 0" />
            </div>
            <p class="p-2 text-xl font-bold pointer-events-none bg-slate-200">
              {{ countThree }}
            </p>
          </div>
        </div>
        <div class="relative overflow-hidden size-1/2">
          <button
            @click="countFour++"
            type="button"
            class="relative transition-opacity duration-300 origin-center scale-150 rotate-45 -translate-x-1/2 -translate-y-1/2 bg-yellow-500 touch-manipulation -top-3 size-full transform-gpu hover:opacity-70"
          ></button>
          <div
            v-if="countFour"
            class="absolute -rotate-45 -translate-x-1/2 -translate-y-1/2 top-1/2 left-1/2"
          >
            <div
              class="absolute -translate-x-1/2 translate-y-2 top-full left-1/2"
            >
              <base-button text="reset" @click="countFour = 0" />
            </div>
            <p class="p-2 text-xl font-bold pointer-events-none bg-slate-200">
              {{ countFour }}
            </p>
          </div>
        </div>
      </div>
      <base-button
        v-if="areMultipleClicked"
        text="Reset All"
        @click="resetAll"
      />
    </div>
  </div>
</template>
