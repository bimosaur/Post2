<script setup>
import { ref, onMounted } from 'vue';
import PocketBase from 'pocketbase';

const pb = new PocketBase('http://127.0.0.1:8090');
const titleVal = ref("");
const data = ref([])

async function submit(){
    const record = {
    Title: titleVal.value,
    Description: "desc",
};

   await pb.collection('post2').create(record);
   data.value.push(record);
}

onMounted(async () => {
    const result = await pb.collection("post2").getFullList();
    data.value = result;
});

</script>

<template>
<input v-model="titleVal"/>
<button @click="submit">Submit</button>

<ul>
    <li v-for="item in data">
        {{ item.Title }}
    </li>
</ul>

</template>