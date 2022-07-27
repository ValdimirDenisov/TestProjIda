<template>
    <div class="left">
        <slot></slot>
    </div>
</template>

<script>
export default {
    name: "SecondContainer"
}
</script>

<style lang="sass" scoped>
    .left
        margin-bottom: 20px
    @media (min-width: 700px)
        .left
            max-width: 348px
            padding: 8px
            margin-bottom: 0


</style>