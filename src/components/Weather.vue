<template>
    <div>
    <transition mode="out-in">
      <h2 v-if="temperature == null">???</h2>
      <h2 v-else>{{ temperature }}&deg;</h2>
    </transition>
    </div>
</template>

<script>
export default {
    props: ['temperature'],
}
</script>

<style scoped>
h2 {
    margin-top: 50px;
    font-size: 200px;
}

.v-enter-from, .v-leave-to {
    opacity: 0;
    transform: rotate(180deg);
}

.v-leave-to {
    transform: rotate(360deg);
}

.v-enter-active {
    transition: all 0.3s ease-out;
}

.v-leave-active {
    transition: all 0.3s ease-in;
}

.v-enter-to, .v-leave-from {
    opacity: 1;
    transform: rotate(360deg);
}
</style>