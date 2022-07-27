<template>
    <div class="parent">
        <div class="sort">
            <select class="sorter" @change="$emit('changeSort', typeSort)" v-model="typeSort">
                <option value="0" >По умолчанию</option>
                <option value="1">По цене ↑</option>
                <option value="2" selected="selected">По цене ↓</option>
                <option value="3">По назвванию</option>
            </select>
        </div>
    </div>
</template>

<script>
export default {
    name: "SortSelect",
    data() {
        return {
            typeSort: 0
        }
    }
}
</script>

<style scoped lang="sass">
    .parent
        width: 100%
        height: 73px

    .sort
        margin-left: calc(100% - 145px)
        @media (max-width: 500px)
            margin-left: calc(100% - 135px)
        margin-top: 25px
        display: inline-block
        height: 36px
        .sorter
            height: 36px
            //padding: 16px
            border: none
            color: #B4B4B4
            background: #FFFEFB
            box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1)
            border-radius: 4px
            font-family: Source Sans Pro, sans-serif
            font-size: 12px
            font-style: normal
            font-weight: normal
            line-height: 15px
            padding: 10px 16px 11px 16px
        .sorter:focus
            outline: none

</style>
