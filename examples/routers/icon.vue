<template>
    <div>
        <Icon type="android-search" hoverType="arrow-return-left"  size="25" color="green" v-on:click="click"></Icon>
        <Button type="primary" shape="circle" icon="ios-search"  hoverIcon="checkmark"></Button>
        <Button type="primary" shape="circle" icon="ios-search" ></Button>
    </div>

</template>
<script>
    export default {
        methods:{
            click(){
                console.info("click ")
            }
        }
    }
</script>