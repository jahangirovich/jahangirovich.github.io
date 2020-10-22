<template>
  <div class="main">
    <Header></Header>
    <div class="main__blocks">
      <div class="main__blocks__header">
        <span>Уход и гигиена</span>
      </div>
      <div class="main__blocks__divide">
        <div class="menu">
      <div class="menu__blocks">
          <div v-for="(item,i) in categories" 
                :key="i"
                :class="'menu__blocks__item '+i">
                    <div class="menu__blocks__item__header" @click="openOptions(i)">
                        <p>{{ item.title }}
                            <span class="cover">
                                <i class="arrow right"></i>
                            </span>
                          </p>
                    </div>
                    <div class="menu__blocks__item__blog" 
                          :style="stylesses[`styles${i}`]">
                        <div class="menu__blocks__item__blog__categories" 
                        v-for="(category,i) in item.options" 
                        :key="i"
                        @click="filterBy(item.name,category)"
                        >
                          <div class="menu__blocks__item__blog__categories__texts">
                              <span>{{ category }}</span>
                          </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="items">
          <Item
                v-for="(item,i) in items" 
                :key="i"
                :item="item">
          </Item>
        </div>
      </div>
      <div class="main__blocks__buttons">
        <div class="custom_button" 
        v-for="item in max_pages" 
        :key="item"
        @click="paginate(item)">
          {{ item }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Header from './Header.vue'
import Item from './Item.vue'
import axios from 'axios'
export default {
  name: 'Main',
  
  components:{
    Header,
    Item,
  },
  data(){
    return{
      categories:[],
      items:[],
      max_pages:undefined,
      curPage:1,
      paginVal:"",
      name:"",
      url:"https://mava.a-lux.dev/api/",
      stylesses:{
          "styles0":{
              height: 0,
          },
          "styles1":{
              height: 0,
          }
      },
      flag:{0:false,1:false}
    }
  },
  props: {
    msg: String
  },
  mounted(){
    axios.get(`${this.url}filters`)
      .then((val)=>{
        this.categories = val.data["data"]
      });
    axios.get(`${this.url}products?page=${1}`)
      .then((val) =>{
        this.items = val.data["products"]
        this.max_pages = val.data["products"]["total_pages"]
      })
      
  },
  methods:{
      paginate(i){
        this.curPage = i
         axios.get(`${this.url}products?page=${i}&${this.name}=${this.paginVal}`)
          .then((val) =>{
            this.items = val.data["products"]
            console.log(val)
            this.max_pages = val.data["products"]["total_pages"]
          })
          .catch((val)=>{
            console.log(val)
          })
      },
      filterBy(name,paginVal){
        axios.get(`${this.url}products?page=1&${name}=${paginVal}`)
        .then((val) =>{
          this.items = val.data["products"]
          this.max_pages = val.data["products"]["total_pages"]
        })
        .catch((val)=>{
          console.log(val)
        })
        this.name = name
        this.paginVal = paginVal
      },
      openOptions(id){
            if(this.flag[id]) this.stylesses[`styles${id}`].height = "0"
            else this.stylesses[`styles${id}`].height = "100%"
            this.flag[id] = !this.flag[id]
        }
  },
  
}
</script>
<style lang="sass" scoped>
  @import '../styles/_blocks.sass'
  @import '../styles/Pagination.sass'
  @import '../styles/_item_style.sass'
  @import '../styles/_category_style.sass'
</style>