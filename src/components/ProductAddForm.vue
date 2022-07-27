<template>
    <div class="form_wrapper">
        <form action="">
            <div class="action_input" >
                <label>Наименование товара<span style="color: red">*</span></label>
                <input :class="{ warning_inp: !named && flagTouch}" placeholder="Введите наименование товара" type="text" v-model="named">
                <label v-if="!named && flagTouch" class="warning">Поле является обязательным</label>
            </div>

            <div class="action_input">
                <label>Описание товара </label>
                <textarea placeholder="Введите описание товара" class="text_area" cols="30" rows="10" v-model="description"></textarea>
            </div>

            <div class="action_input">
                <label>Ссылка на изображение товара <span style="color: red">*</span></label>
                <input :class="{ warning_inp: !src_img && flagTouch}" placeholder="Введите ссылку" type="text" v-model="src_img">
                <label v-if="!src_img && flagTouch" class="warning">Поле является обязательным</label>
            </div>

            <div class="action_input">
                <label>Цена товара<span style="color: red">*</span></label>
                <input :class="{ warning_inp: !price && flagTouch}"  placeholder="Введите цену" type="text" @blur="OnBlurPrice" @focus="OnFocusPrice" v-model="price">
                <label v-if="!price && flagTouch" class="warning">Поле является обязательным</label>
            </div>
            <input v-if="FormValid" class="button active" @click="addProduct"  value="Добавить товар">
            <div v-else class="button disable" @click="flagTouch = true"> <p style="padding-top: 10px">Добавить товар</p></div>
        </form>
    </div>
</template>

<script>
export default {
    name: "ProductAddForm",
    data() {
        return {
            'named': '',
            'src_img': '',
            'price': '',
            'description': '',
            'FormValid': false,
            'flagTouch': false,
        }
    },
    methods: {
        OnFocusPrice(e) {
            let target = e.target
            target.value = e.target.value.split(' ').join('')
        },
        OnBlurPrice(e) {
            let target = e.target
            target.value = e.target.value.replace(/(\d{1,3}(?=(?:\d\d\d)+(?!\d)))/g, "$1" + ' ')
        },
        addProduct() {
            let item = {
                'name': this.named,
                'description': this.description,
                'price': this.price.replace(/(\d{1,3}(?=(?:\d\d\d)+(?!\d)))/g, "$1" + ' '),
                'src': this.src_img
            }
            this.src_img = ''
            this.price = ''
            this.description = ''
            this.named = ''
            this.flagTouch = false
            this.$emit('addProduct', item)
        }
    },
    watch: {
        named: function () {
            this.FormValid = this.named && this.price && this.src_img
        },
        src_img: function () {
            this.FormValid = this.named && this.price && this.src_img
        },
        price: function () {
            this.price = this.price.replace(/[^\d]+/g,'')
            this.FormValid = this.named && this.price && this.src_img
        },
    }
}
</script>

<style lang="sass" scoped>
    @import url('https://fonts.googleapis.com/css2?family=Inter:wght@600&display=swap')
    .form_wrapper
        @media (max-width: 700px)
            margin: 8px
        width: 332px
        height: 440px
        text-align: center
        background: #FFFEFB
        box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02)
        border-radius: 4px
        padding: 24px
        box-sizing: border-box

        .action_input
            text-align: left
            margin-bottom: 16px
            width: 284px
            label
              display: block
              margin-bottom: 4px
            .warning
              //display: block
              //position: relative
              //top: 4px
              margin-bottom: -17px
              margin-top: 4px
              color: #FF8484
              font-family: Source Sans Pro, sans-serif
              font-style: normal
              font-weight: 400
              font-size: 8px
              line-height: 10px
            .warning_inp
              border: 1px solid #FF8484


            .text_area
                outline: none
                resize: none
                width: calc(284px - 32px)
                height: calc(108px - 20px)
                background: #FFFEFB
                box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1)
                border-radius: 4px
                border: none
            .text_area[placeholder]
              text-overflow: ellipsis
              padding: 10px 16px
              font-weight: 400
              line-height: 15px
              letter-spacing: 0em
              font-size: 12px
              font-family: Source Sans Pro, sans-serif

        input:active
            border: none


        input
            width: calc(284px - 32px)
            height: calc(36px - 20px)
            background: #FFFEFB
            box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1)
            border-radius: 4px
            border: none
        input[placeholder]
          text-overflow: ellipsis
          padding: 10px 16px
          font-size: 12px

        input:focus
            outline: none
        label
            font-size: 10px
            height: 13px
        .button
            margin-top: 8px
            width: 284px
            height: 36px
            font-family: 'Inter'
            text-align: center
            font-size: 12px
            border-radius: 10px
            cursor: pointer
            color: #B4B4B4
            background-color: #EEEEEE
            font-style: normal
            font-weight: 600
            line-height: 15px
            letter-spacing: -0.02em
            cursor: initial
            box-shadow: none


        .active
            background-color: #7bae73
            transition: 1s ease-out
            color: white
            cursor: pointer
        .active:hover
            background-color: #95ff8a
</style>
