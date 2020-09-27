<template>
  <header class="p-5 lg:p-10 mb-5 container mx-auto">
    <h1 class="font-bold text-3xl leading-tight mb-3">
      Convert <code>HH:MM:SS</code> to decimal hours.
    </h1>
    <p class="text-teal-500">
      A handy tool built to make exporting time entries out of Toggl and into
      Harvest just a little bit smoother.
    </p>
  </header>
  <main
    class="container mx-auto px-5 lg:px-10 flex flex-col md:flex-row justify-between space-y-5 md:space-y-0 md:space-x-10"
  >
    <div class="flex flex-col w-full">
      <label for="hours"
        >Paste your <strong>HH:MM:SS</strong> values here.</label
      >
      <textarea
        id="hours"
        cols="1"
        rows="25"
        v-model="hours"
        class="border border-gray-300 px-3 py-2"
      ></textarea>
    </div>

    <div class="flex flex-col w-full">
      <label for="hours">Converted decimal values.</label>
      <textarea
        id="hours"
        cols="1"
        rows="25"
        class="border border-gray-300 px-3 py-2"
        :value="converted"
        readonly
      ></textarea>
    </div>
  </main>
  <h1></h1>
</template>

<script>
import { ref, computed } from "vue";
export default {
  name: "App",
  setup() {
    const hours = ref("");

    const convertAndRound = (hours, minutes, seconds) =>
      hours + minutes / 60 + seconds / 3600;

    const converted = computed(() => {
      if (hours.value) {
        return hours.value
          .split("\n")
          .map((timeString) => {
            const [hours, minutes, seconds] = timeString
              .split(":")
              .map((val) => parseInt(val));

            return convertAndRound(hours, minutes, seconds);
          })
          .join("\n");
      }

      return null;
    });

    return {
      hours,
      converted,
    };
  },
};
</script>
