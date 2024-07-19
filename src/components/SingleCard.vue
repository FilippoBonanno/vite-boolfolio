<script>
export default {
    props: ["card"],

    data() {
        return {
            base_url: 'http://localhost:8000',
        }
    }
}
</script>

<template>

    <div class="card" style="width: calc(100% / 3);">
        <template v-if="!card.img.startsWith('http')">
            <img class="card-img-top" :src="base_url + '/storage/' + card.img" alt="">

        </template>
        <template v-else>
            <img class="card-img-top" :src="card.img" alt="">
        </template>
        <div class="card-body">
            {{ card.title }}
        </div>
    </div>
</template>

<style scoped></style>