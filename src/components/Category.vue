<template>
  <div>

  </div>
</template>

<script>
export default {
    name:"Category",
    data(){
        return{
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
    props:[
        "array"
    ],
    methods:{
        openOptions(id){
            if(this.flag[id]) this.stylesses[`styles${id}`].height = "0"
            else this.stylesses[`styles${id}`].height = "100%"
            this.flag[id] = !this.flag[id]
        }
    }
}
</script>

<style lang="sass">
    @import '../styles/_category_style.sass'
</style>