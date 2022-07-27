<template>
    <div class="main">
        <slot></slot>
    </div>
</template>

<script>
export default {
    name: "MainConteiner"
}
</script>

<style lang="sass" scoped>
    .main
        display: flex
        flex-flow: row wrap
        justify-content: flex-start
        min-width: 348px
        max-width: 1050px
        @media (max-width: 1400px)
            //justify-content: center
</style>
