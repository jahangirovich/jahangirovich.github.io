<template>
    <div class="items">
        <Item
                v-for="(item,i) in items" 
                :key="i"
                :item="item"
                v-on:click.native="filterBy(item)">
        </Item>
    </div>
</template>

<script>
export default {
    name:"Items",
    
}
</script>

<style lang="sass" scoped>
    
</style>