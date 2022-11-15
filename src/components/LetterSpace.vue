<template>
  <div id="letter-space">
    <h1 class="space-one" v-if="spaceNumber == 1">
        {{ this.$store.state.selectedLetter1 }}
    </h1>
    <h1 class="space-two" v-if="spaceNumber == 2">
        {{ this.$store.state.selectedLetter2 }}
    </h1>
    <h1 class="space-three" v-if="spaceNumber == 3">
        {{ this.$store.state.selectedLetter3 }}
    </h1>
    <h1 class="space-four" v-if="spaceNumber == 4">
        {{ this.$store.state.selectedLetter4 }}
    </h1>
    <h1 class="space-five" v-if="spaceNumber == 5">
        {{ this.$store.state.selectedLetter5 }}
    </h1>
  </div>
</template>

<script>
export default {
    name: "letter-space",
    props: ["spaceNumber"],
}
</script>

<style scoped>
.space-one, .space-two, .space-three, .space-four, .space-five {
    text-transform: uppercase;
    font-size: 3rem;
}

</style>