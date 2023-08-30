<script setup lang="ts">
const result = ref<{ date: string }>({ date: new Date().toString() });
onMounted(async () => {
  while (true) {
    await new Promise(async (resolve) => await setTimeout(async () => {
      const response = await $fetch("/api/time", {
        method: "get"
      });
      if (response) {
        result.value = response;
      }
      resolve(2500);
    }, 2500));
  }
});  
</script>

<template>
  <div>
    {{ new Date(result?.date).toString() }}
  </div>
</template>
