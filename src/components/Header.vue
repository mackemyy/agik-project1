<script lang="ts">
import { useCurrentTime } from "../composables/useCurrentTime";

    export default {
    name: "Header",
    setup() {
        const { currentTime } = useCurrentTime();
        console.log(currentTime.value);
        return { currentTime };
    },
};
</script>

<template>
    <div class="flex items-start justify-center pt-6">
        <div class="flex justify-center items-center gap-5">
            <div class="p-7 bg-white rounded-2xl ">
                <p class="font-medium text-purple-500 pt-3 text-3xl">{{ currentTime.toLocaleTimeString() }}</p>
                <p class="font-medium text-pink-500 text-[10px] mb-1 flex justify-end mr-3">{{ currentTime.toLocaleDateString() }}</p>
            </div>
            <p class="font-sans font-bold text-3xl text-white">TO DO LIST</p>
        </div>
    </div>
</template> 