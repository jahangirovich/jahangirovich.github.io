<template>
<div class="itemBlog" v-if="item.date!==undefined">
    <div class="itemBlog__header">
        <div class="itemBlog__header__produced">
            <span class="text">{{ item.date === undefined?'free':item.date }}</span>
        </div>
    </div>
    <div class="itemBlog__imageBlog">
        <img src="../assets/img/product-page/image.png" alt="">
    </div>
    <div class="itemBlog__body">
        <p class="title">
            {{ item.title }}
        </p>
        <p class="quantity">
            Есть на складе: {{ item.in_stock }}
        </p>
    </div>
    <div class="itemBlog__footer">
        <div class="itemBlog__footer__price">
            <p class="real_price">
                {{ item.price }} тг.
            </p>
            
        </div>
    </div>
</div>
</template>

<script>
export default {
    name:"Item",
    props:["item"]
}
</script>

<style lang="sass">
    @import '../styles/item.sass'
</style>