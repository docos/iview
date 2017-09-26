<template>
    <div style="border: solid 1px red;width: 100%;height: 1000px;" @contextmenu.prevent="openMenu">
        <div id="right-click-menu" tabindex="-1" ref="right" v-if="viewMenu" @blur="closeMenu"  :style="{top:top, left:left}">
            <Dropdown-menu slot="list" @on-click="handleClick">
                <Dropdown-item name=1 :bubbling="true"><Icon type="checkmark" /> <span>驴打滚</span></Dropdown-item>
                <Dropdown-item name=2 :bubbling="true"><Icon type="checkmark" /><span>炸酱面</span></Dropdown-item>
                <Dropdown-item name=3 :bubbling="true"><span class="noicon" >豆汁儿</span></Dropdown-item>
                <div class="separator"></div>
                <Dropdown :placement="subItemPlace" @on-click="handleClick">
                    <Dropdown-item>
                        <Icon type="checkmark" />
                        <span>北烤鸭</span>
                        <Icon type="ios-arrow-right" style="float: right"></Icon>
                    </Dropdown-item>
                    <Dropdown-menu slot="list">
                        <Dropdown-item name=4><Icon type="checkmark" /><span>炉烤鸭</span></Dropdown-item>
                        <Dropdown-item name=5><span class="noicon">炉烤鸭</span></Dropdown-item>
                    </Dropdown-menu>
                </Dropdown>
                <Dropdown-item name=6><Icon type="checkmark" /><span>冰糖葫芦</span></Dropdown-item>
            </Dropdown-menu>
        </div>
    </div>


</template>
<script>
    export default {
        ame: 'my-component',
        data() {
            return {
                viewMenu: false,
                subItemPlace:"right-start",
                top: '0px',
                left: '0px'
            }
        },
        methods: {
            setMenu: function(top, left) {

                let largestHeight = window.innerHeight - this.$refs.right.offsetHeight - 25;
                let largestWidth = window.innerWidth - this.$refs.right.offsetWidth - 25;
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

            closeMenu: function() {
                this.viewMenu = false;
            },

            openMenu: function(e) {
                this.viewMenu = true;

                this.$nextTick(() =>{
                    this.$refs.right.focus();
                    this.setMenu(e.y, e.x)
                });
                e.preventDefault();
            },
            handleClick:function(value){
                console.info("click ",value)
                this.viewMenu = false;
            }
        }
    }
</script>
<style>

    #right-click-menu{
        background: transparent;
        border: none !important;
        -webkit-border-radius: 2px;
        border-radius: 2px;
        -webkit-box-shadow: 0 8px 10px 1px rgba(0,0,0,0.14), 0 3px 14px 2px rgba(0,0,0,0.12), 0 5px 5px -3px rgba(0,0,0,0.2);
        box-shadow: 0 8px 10px 1px rgba(0,0,0,0.14), 0 3px 14px 2px rgba(0,0,0,0.12), 0 5px 5px -3px rgba(0,0,0,0.2);
        -webkit-transition: height 267ms cubic-bezier(0.4,0.0,0.2,1) 0ms,margin-top 267ms cubic-bezier(0.4,0.0,0.2,1),opacity 267ms cubic-bezier(0.4,0.0,0.2,1);
        transition: height 267ms cubic-bezier(0.4,0.0,0.2,1) 0ms,margin-top 267ms cubic-bezier(0.4,0.0,0.2,1),opacity 267ms cubic-bezier(0.4,0.0,0.2,1);
        will-change: height,margin-top,opacity;
        display: block;
        margin: 0;
        padding: 0;
        position: absolute;
        width: 320px;
        z-index: 999999;
        padding-top: 16px;
        padding-bottom: 16px;
    }
    #right-click-menu:focus{
        outline-color: transparent !important;;
    }
    #right-click-menu .separator{
        border-bottom: 1px solid #E0E0E0;
        margin-top: 8px;
        margin-bottom: 8px;
    }
    #right-click-menu li {
        /*border-bottom: 1px solid #E0E0E0;*/
        margin: 0;
        width: 320px;
    }
    #right-click-menu li span{
       margin-left: 20px;
        font-size: 16px;
    }
    #right-click-menu .noicon{
        margin-left: 32px;
    }
    #right-click-menu li:last-child {
        border-bottom: none;
    }

    #right-click-menu li:hover {
        background: rgba(0,0,0,.06);;
        /*color: #FAFAFA;*/
    }
</style>
