<script setup>






onMounted(async () => {
    var response = await fetch("/api/bookings/stats/superhero");
    var json = await response.json();
    options.value = { labels: json.map((item) => item._id) };
    series.value = json.map((item) => item.total);
});


import { ref, onMounted, defineProps } from "vue";

const props = defineProps({
    team: String,
});

const options = ref({});
const series = ref([]);

onMounted(async () => {
    var response = await fetch("/api/bookings/stats/superhero?team=" + props.team);
    var json = await response.json();
    options.value = {
        labels: json.map((item) => item._id),
        title: { text: props.team || "All Teams" }
    };
    series.value = json.map((item) => item.total);
});

</script>

<template>
    <div>
        <apexchart type="donut" :options="options" :series="series" />
    </div>
</template>


<style scoped>

</style>

import { ref, onMounted } from "vue";

const options = ref({});
const series = ref([]);

onMounted(async () => {
    var response = await fetch("/api/bookings/stats/superhero");
    var json = await response.json();
    options.value = { labels: json.map((item) => item._id) };
    series.value = json.map((item) => item.total);
});
