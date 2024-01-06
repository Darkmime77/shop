<template>
    <div class="navigation">
        <div class="container nav__cont">
            <a><img src="../assets/logo.png" alt=""></a>
            <div class="nav__main">
                <div class="nav__button" style='width: 25%;text-align: center;'>
                    <a class="nav__main-page">Главная</a>
                    <div class="line__main line" style="width: 100%;"></div>
                </div>
                <div class="nav__button">
                    <a class="nav__shop">Магазин</a>
                    <div class="line__shop line"></div>
                </div>
                <div class="nav__button">
                    <a class="nav__supp">Поддержка</a>
                    <div class="line__supp line"></div>
                </div>
                <div class="nav__button">
                    <a class="nav__about">О нас</a>
                    <div class="line__about line"></div>
                </div>
            </div>
            <div class="log__btn">
                <a class="nav__login">Вход</a>
                <div class="line__login line"></div>
            </div>
            <div class="nav__phone-btn">
            </div>
        </div>
    </div>
    <div class="selector">
        <select v-model="selector" @change="()=>
        {
            url = `https://fakestoreapi.com/products${razdel[selector]}`
            getWeather()
        }">
            <option value="0">all</option>
            <option value="1">men's clothing</option>
            <option value="2">jewelery</option>
            <option value="3">electronics</option>
            <option value="4">women's clothing</option>
        </select>
    </div>
    <div class="products">
        <Product @openens="openeers" v-for="index in indicate" v-bind:key="index" :name="name[index-1+indexPop]" 
        :price="price[index-1+indexPop]" :desc="desc[index-1+indexPop]" :cat="cat[index-1+indexPop]" 
        :image="image[index-1+indexPop]" :rate="rate[index-1+indexPop]" :count="count[index-1+indexPop]"/>
    </div>
    <div class="Numbers" v-if = "list.length >= 10">
        {{ chil() }}
        <input type="button" :value="linenins" v-for="linenins in indexs" v-bind:key="linenins" @click="()=>{
            indexPop = (linenins - 1) * 10
        }">
    </div>
    <modal
      v-show="isModalVisible"
      @close="closeModal"
      :name = "lname"
      :count="lcount"
      :desc="ldesc"
      :price="lprice"
      :cat="lcat"
      :image="limage"
      :rate="lrate" 
    />
</template>
<script>
import Product from './productCart.vue'
import modal from './modal.vue'
export default {
    name: 'TestOps',
    components: {
        Product,
        modal
    },
    data() {
        return {
            isModalVisible: false,
            list: 0,
            lname: "",
            lprice: "",
            ldesc: "",
            lcat: "",
            indicate: 0,
            linenins: 0,
            limage: "",
            lrate: "",
            lcount: "",
            indexs: 0,
            name: [],
            price: [],
            desc: [],
            cat: [],
            image: [],
            rate: [],
            count: [],
            razdel: ["","/category/men's clothing", "/category/jewelery", "/category/electronics", "/category/women's clothing"],
            indexPop: 0,
            selector: 0,
            url: "https://fakestoreapi.com/products",
        };
    },
    methods: {
        chil(){
            this.indexs
            this.indexs = Math.ceil(this.list.length / 10)
        },
        openeers(name, price, desc, cat, image, rate, count){
            this.lname = name
            this.lprice = price
            this.ldesc = desc
            this.lcat = cat
            this.limage = image
            this.lrate = rate
            this.lcount = count
            this.showModal()
        },
        showModal() {
            this.isModalVisible = true;
        },
        closeModal() {
            this.isModalVisible = false;
        },
        getWeather() {
            this.name = []
            this.price = []
            this.desc = []
            this.cat = []
            this.image = []
            this.count = []
            this.rate = []
            fetch(this.url).then(res => res.json()).then((json) => {
                    this.list = json
                    for (let i in this.list)
                    {
                        this.name.push(this.list[i]["title"])
                        this.price.push(this.list[i]["price"])
                        this.desc.push(this.list[i]["description"])
                        this.cat.push(this.list[i]["category"])
                        this.image.push(this.list[i]["image"])
                        this.count.push(this.list[i]["rating"]["count"])
                        this.rate.push(this.list[i]["rating"]["rate"])
                    }
                    if (this.list < 10){
                        this.indicate = 10
                    }
                    else{
                        this.indicate = this.list.length
                    }
                })
        },
    },
    mounted() {
        this.getWeather();
    },
}
</script>
<style>
.products {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    gap: 3%;
    row-gap: 30px;
}

.selector{
    padding: 20px;
}

.nav__a:hover {
    color: #b2b0b0;
}

.navigation {
    width: 100%;
}

.nav__cont {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
    z-index: 5;
    align-items: center;
    width: 100% !important;
}

.nav__cont img {
    width: 215px;
    height: 70px;
}

.nav__cont a {
    text-decoration: none;
    color: black;
    text-align: center;
    font-family: 'TLheader';
    font-size: 24px;
    font-style: normal;
    font-weight: 700;
    line-height: normal;
    text-decoration: 0;
    text-decoration: none;
}

.navigation a:hover {
    color: black;
    text-decoration: none;
}

.nav__main {
    width: 45%;
    display: flex;
    flex-direction: row;
    justify-content: space-between;
}
</style>