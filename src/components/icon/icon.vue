<template>
    <i :class="classes" :style="styles" @mouseover="hover" @mouseleave="blur" @click="click"></i>
</template>
<script>
    const prefixCls = 'ivu-icon';

    export default {
        name: 'Icon',
        props: {
            type: String,
            hoverType:String,
            size: [Number, String],
            color: String
        },
        data(){
            return {
                focused:false,
            }
        },
        computed: {
            classes () {
                if(!this.focused || !this.hoverType){
                    return `${prefixCls} ${prefixCls}-${this.type}`;
                }else{
                    return `${prefixCls} ${prefixCls}-${this.hoverType}`;
                }

            },
            styles () {
                let style = {};

                if (this.size) {
                    style['font-size'] = `${this.size}px`;
                }

                if (this.color) {
                    style.color = this.color;
                }

                return style;
            }
        },
        methods:{
            hover(){
                if(!this.hoverType){
                    return;
                }
                this.focused = true;
            },
            blur(){
                if(!this.hoverType){
                    return;
                }
                this.focused = false;
            },
            click(){
                this.$emit("click")
            }
        }
    };
</script>
