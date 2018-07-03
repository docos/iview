<style>
    .demo-breadcrumb-separator{
        color: #ff5500;
        padding: 0 5px;
    }
</style>
<template>
<div>
    <Breadcrumb separator="<b class='demo-breadcrumb-separator'>=></b>">
        <Breadcrumb-item to="/" class="hover" @dragging="dragging" :class="[{dragging:draggingOn},'hover']">Home4</Breadcrumb-item>
        <Breadcrumb-item :to="{name: 'user', params: { userId: 123 }}">Components</Breadcrumb-item>
        <Breadcrumb-item :bubbling="true" @clickItem="handleCall(123)">Breadcrumb</Breadcrumb-item>
    </Breadcrumb>
    <Breadcrumb separator="">
        <Breadcrumb-item href="/">
            <template>Home</template>
            <template slot="separator">
                <b style="color: #ff5500;">-></b>
            </template>
        </Breadcrumb-item>
        <Breadcrumb-item href="/components/page">
            <template>Breadcrumb</template>
            <template slot="separator">
                <b style="color: #ff5500;">-></b>
            </template>
        </Breadcrumb-item>
        <Breadcrumb-item>Breadcrumb</Breadcrumb-item>
    </Breadcrumb>
    <img src="http://kspservice:9000/static/742.jpg" @dragstart="dragstart_handler"/>
</div>
</template>
<script>
    export default {
        data(){
          return {
              draggingOn:false
          }
        },
        methods: {
            handleCall(args){
                console.info("click!",args);
            },
            dragstart_handler(ev) {
                console.log("dragStart");
                var img = new Image();
                img.src = 'http://kspservice:9000/static/avatar/6999f120_avatar.png';
                ev.dataTransfer.setDragImage(img, 10, 10);
            },
            dragging( status){
                console.info("dragging on ",status)
                this.draggingOn = status;
            }
        }
    }
</script>
<style lang="less">
    .hover:hover{
        background-color: gold;
    }
    .dragenter{
        background-color: gold;
    }
</style>