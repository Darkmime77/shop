<template>
    <div class="products__product">
        <div class="products__imgs">
            <img :src="image" alt="Товар" class="products__img">
        </div>
        <div class="products__price">
            <h2>{{ price }} $</h2>
        </div>
        <div class="products__cat">
            <h3>{{ cat }}</h3>
        </div>
        <div class="products__name">
            <h1>{{ name }}</h1>
        </div>
        <div class="products__rate">
            <p>Рейтинг: {{ rate }}</p>
            <p>Голоса: {{ count }}</p>
        </div>
        <div class="buttons">
            <input type="button" value="Подобнее" @click="open">
        </div>
    </div>
</template>
<script>
export default {
    name: 'productCart',
    props:[
        "name", 
        "price",
        "desc",
        "cat",
        "image",
        "rate",
        "count"],
    methods: {
        open() {
        this.$emit("openens",this.name, this.price, this.desc, this.cat, this.image, this.rate, this.count);
      },
    }
}
</script>
<style lang="css">
    .products__product{
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: space-between;
        padding-top: 15px;
        padding-bottom: 15px;
        width: 22%;
        border: solid 1px black;
    }
    .products__rate{
        width: 80%;
        padding-left: 25px;
        padding-right: 25px;
        display: flex;
        justify-content: space-between;
    }
    .products__img{
        object-fit: contain;
        width: 200px;
        height: 200px;
    }
</style>