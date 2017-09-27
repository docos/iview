<template>
    <div id="right-click-menu" tabindex="-1"  @blur="closeMenu" :style="{top:top, left:left,display:display}">
        <DropdownMenu slot="list" @on-click="handleClick">
            <template v-for="item in items">
                <div class="separator" v-if="item.separator"></div>
                <DropdownItem :name="item.name" :bubbling="true" v-else-if="!item.subs">
                    <template v-if="item.icon">
                        <Icon :type="item.icon"/>
                        <span>{{item.title}}</span>
                    </template>
                    <template v-if="!item.icon">
                        <span class="noicon">{{item.title}}</span>
                    </template>
                </DropdownItem>
                <Dropdown :placement="subItemPlace" @on-click="handleClick" v-else>
                    <DropdownItem>
                        <template v-if="item.icon">
                            <Icon :type="item.icon"/>
                            <span>{{item.title}}</span>
                        </template>
                        <template v-if="!item.icon">
                            <span class="noicon">{{item.title}}</span>
                        </template>
                        <Icon type="ios-arrow-right" style="float: right"></Icon>
                    </DropdownItem>
                    <DropdownMenu slot="list">
                        <DropdownItem v-for="(sub,idx ) in item.subs" :name="sub.name" :key="idx">
                            <template v-if="sub.icon">
                                <Icon :type="sub.icon"/>
                                <span>{{sub.title}}</span>
                            </template>
                            <template v-if="!sub.icon">
                                <span class="noicon">{{sub.title}}</span>
                            </template>
                        </DropdownItem>
                    </DropdownMenu>
                </Dropdown>
            </template>
        </DropdownMenu>
    </div>

</template>
<script>
    import Dropdown from './../../components/Dropdown';
    import Icon from './../../components/Icon';
    export default {
        name: 'context',
        components:{
            Dropdown:Dropdown,
            DropdownMenu:Dropdown.Menu,
            DropdownItem:Dropdown.Item,
            Icon:Icon
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
            items: {
                type: Array,
                default: []
            },
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
                this.viewMenu = false;
            },

            openMenu: function (x,y) {
                this.viewMenu = true;

                this.$nextTick(() => {
                    this.$el.focus();
                    this.setMenu(y, x)
                });
//                e.preventDefault();
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
        background: transparent;
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
        position: relative;
        width: 320px;
        z-index: 999999;
        padding-top: 16px;
        padding-bottom: 16px;
    }

    #right-click-menu:focus {
        outline-color: transparent !important;;
    }

    #right-click-menu .separator {
        border-bottom: 1px solid #E0E0E0;
        margin-top: 8px;
        margin-bottom: 8px;
    }

    #right-click-menu li {
        /*border-bottom: 1px solid #E0E0E0;*/
        margin: 0;
        width: 320px;
    }

    #right-click-menu li span {
        margin-left: 20px;
        font-size: 16px;
    }

    #right-click-menu .noicon {
        margin-left: 32px;
    }

    #right-click-menu li:last-child {
        border-bottom: none;
    }

    #right-click-menu li:hover {
        background: rgba(0, 0, 0, .06);;
        /*color: #FAFAFA;*/
    }
</style>