<template>
    <div style="border: solid 1px red;width: 100%;height: 1000px;" @contextmenu.prevent="openMenu">
        <div id="right-click-menu" tabindex="-1" ref="right" v-if="viewMenu" @blur="closeMenu"  :style="{top:top, left:left}">
            <Dropdown-menu slot="list" @on-click="handleClick">
                <template v-for="item in items">
                    <div class="separator" v-if="item.separator"></div>
                    <Dropdown-item :name="item.name" :bubbling="true" v-else-if="!item.subs">
                        <template v-if="item.icon">
                            <Icon :type="item.icon" />
                            <span>{{item.title}}</span>
                        </template>
                        <template v-if="!item.icon">
                            <span class="noicon" >{{item.title}}</span>
                        </template>
                    </Dropdown-item>
                    <Dropdown :placement="subItemPlace" @on-click="handleClick" v-else>
                        <Dropdown-item >
                            <template v-if="item.icon">
                                <Icon :type="item.icon" />
                                <span>{{item.title}}</span>
                            </template>
                            <template v-if="!item.icon">
                                <span class="noicon" >{{item.title}}</span>
                            </template>
                            <Icon type="ios-arrow-right" style="float: right"></Icon>
                        </Dropdown-item>
                        <Dropdown-menu slot="list">
                            <Dropdown-item v-for="(sub,idx ) in item.subs" :name="sub.name" :key="idx" >
                                <template v-if="sub.icon">
                                    <Icon :type="sub.icon" />
                                    <span>{{sub.title}}</span>
                                </template>
                                <template v-if="!sub.icon">
                                    <span class="noicon" >{{sub.title}}</span>
                                </template>
                            </Dropdown-item>
                        </Dropdown-menu>
                    </Dropdown>
                </template>
            </Dropdown-menu>
        </div>
    </div>
</template>
<script>
    export default {
        name: 'context',
        data() {
            return {
                viewMenu: false,
                subItemPlace:"right-start",
                top: '0px',
                left: '0px'
            }
        },
        props: {
            items:{
                type: Array,
                default: []
            },
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
//                this.viewMenu = false;
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