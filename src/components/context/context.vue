<template>
    <div id="right-click-menu" tabindex="-1"  v-show="viewMenu"  @blur="closeMenu" @click="handleClick"
         @contextmenu.prevent="disableContext"
         :style="{top:top, left:left,width:width+'px'}" :data-transfer="true" v-transfer-dom>
        <slot ></slot>
    </div>

</template>
<script>
    import TransferDom from '../../directives/transfer-dom';
    export default {
        name: 'context',
        directives: { TransferDom },
        components:{

        },
        data() {
            return {
                viewMenu: false,
                subItemPlace: "right-start",
                top: '0px',
                left: '0px'
            }
        },
        props: {
            width:{
                type:Number,
                defalut:100
            },
        },
        methods: {
            setMenu: function (top, left) {

                let largestHeight = window.innerHeight - this.$el.offsetHeight - 25;
                let largestWidth = window.innerWidth - this.$el.offsetWidth - 25;
                if (top > largestHeight) {
                    top = largestHeight;
                }

                if (left > largestWidth) {
                    left = largestWidth;
                }
                this.top = top + 'px';
                this.left = left + 'px';
            },

            closeMenu: function () {
                this.viewMenu = false;
                this.$emit('show',this.viewMenu,this.subItemPlace);
            },

            openContextMenu: function (e) {
                this.viewMenu = true;
                let largestWidth = window.innerWidth - this.width*2 - 25;
                this.subItemPlace = "right-start";
                if (e.x > largestWidth) {
                    this.subItemPlace = "left-start";
                }
                this.$emit('show',this.viewMenu,this.subItemPlace);
                this.$nextTick(() => {
                    this.$el.focus();
                    this.setMenu(e.y, e.x)
                });
                e.preventDefault();
            },
            handleClick: function (event) {
                this.viewMenu = false;
                this.$emit('show',this.viewMenu,this.subItemPlace);
                event && event.preventDefault();
            },
            disableContext:function(event){
                event && event.preventDefault();
            }
        }
    }
</script>
<style>

    #right-click-menu {
        background: white;
        border: none !important;
        -webkit-border-radius: 2px;
        border-radius: 2px;
        -webkit-box-shadow: 0 8px 10px 1px rgba(0, 0, 0, 0.14), 0 3px 14px 2px rgba(0, 0, 0, 0.12), 0 5px 5px -3px rgba(0, 0, 0, 0.2);
        box-shadow: 0 8px 10px 1px rgba(0, 0, 0, 0.14), 0 3px 14px 2px rgba(0, 0, 0, 0.12), 0 5px 5px -3px rgba(0, 0, 0, 0.2);
        -webkit-transition: height 267ms cubic-bezier(0.4, 0.0, 0.2, 1) 0ms, margin-top 267ms cubic-bezier(0.4, 0.0, 0.2, 1), opacity 267ms cubic-bezier(0.4, 0.0, 0.2, 1);
        transition: height 267ms cubic-bezier(0.4, 0.0, 0.2, 1) 0ms, margin-top 267ms cubic-bezier(0.4, 0.0, 0.2, 1), opacity 267ms cubic-bezier(0.4, 0.0, 0.2, 1);
        will-change: height, margin-top, opacity;
        display: block;
        margin: 0;
        padding: 0;
        position: absolute;
        z-index: 999999;
        padding-top: 16px;
        padding-bottom: 16px;
    }

    #right-click-menu:focus {
        outline-color: transparent !important;;
    }
</style>