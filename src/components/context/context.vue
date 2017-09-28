<template>
    <div id="right-click-menu" tabindex="-1"  @blur="closeMenu"
         :style="{top:top, left:left,display:display}" :data-transfer="true" v-transfer-dom>
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
        },
        computed: {
            display: function () {
                if(this.viewMenu){
                    return ""
                }else{
                    return "none"
                }
            }
        },
        methods: {
            setMenu: function (top, left) {

                let largestHeight = window.innerHeight - this.$el.offsetHeight - 25;
                let largestWidth = window.innerWidth - this.$el.offsetWidth - 25;
                this.subItemPlace = "right-start";
                if (top > largestHeight) {
                    top = largestHeight;
                }

                if (left > largestWidth) {
                    left = largestWidth;
                    this.subItemPlace = "left-start";
                }

                this.top = top + 'px';
                this.left = left + 'px';
            },

            closeMenu: function () {
//                this.viewMenu = false;
            },

            openMenu: function (e) {
                this.viewMenu = true;

                this.$nextTick(() => {
                    this.$el.focus();
                    this.setMenu(e.y, e.x)
                });
                e.preventDefault();
            },
            handleClick: function (value) {
                console.info("click ", value);
                this.viewMenu = false;
                this.$emit("selectItem",value)
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
        width: 320px;
        z-index: 999999;
        padding-top: 16px;
        padding-bottom: 16px;
    }

    #right-click-menu:focus {
        outline-color: transparent !important;;
    }
</style>