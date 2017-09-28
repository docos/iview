<template>
    <div style="border: solid 1px red;width: 1800px;height: 800px;position: absolute;left: 100px;top: 100px;"
         @contextmenu.prevent="openContextMenu">
        <Context ref="context" :subItemPlace="subItemPlace" @show="showContext" :width="320">
            <div v-if="isShow">
                <DropdownMenu slot="list" @on-click="handleClick" class="menu">
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
        </Context>

    </div>

</template>
<script>
    export default {
        ame: 'my-component',
        components:{
        },
        data() {
            return {
                items: [{icon: "checkmark", name: 1, title: "驴打滚"},
                    {icon: "checkmark", name: 2, title: "炸酱面"},
                    {name: 3, title: "豆汁儿"},
                    {separator: true},
                    {
                        icon: "checkmark", title: "北烤鸭",
                        subs: [
                            {name: 4, title: "炉烤鸭"},
                            {icon: "checkmark", name: 5, title: "炉烤鸭"}
                        ]
                    },
                    {icon: "checkmark", name: 6, title: "冰糖葫芦"}
                ],
                subItemPlace: "right-start",
                isShow:false
            }
        },
        methods: {
            openContextMenu(event) {
                event && event.preventDefault();
                this.$refs.context.openContextMenu(event)
            },
            handleClick(value){
                console.info("select item ", value)
            },
            showContext(isShow,subItemPalce){
                this.isShow = isShow;
                this.subItemPlace = subItemPalce;
            }
        }
    }
</script>
<style lang="less">
    .menu{
        .separator {
            border-bottom: 1px solid #E0E0E0;
            margin-top: 8px;
            margin-bottom: 8px;
        }

        li {
            /*border-bottom: 1px solid #E0E0E0;*/
            margin: 0;
            width: 320px;
        }

        li span {
            margin-left: 20px;
            font-size: 16px;
        }

        .noicon {
            margin-left: 32px;
        }

        li:last-child {
            border-bottom: none;
        }

        li:hover {
            background: rgba(0, 0, 0, .06);;
            /*color: #FAFAFA;*/
        }
    }

</style>
