<template>
    <div style="border: solid 1px red;width: 100%;height: 1000px;position: absolute;left: 100px;top: 100px;" @contextmenu.prevent="openContextMenu" >
        <Context :items="items" ref="context" @selectItem="handleSelect">

        </Context>

    </div>

</template>
<script>
    export default {
        ame: 'my-component',
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
                ]
            }
        },
        methods: {
            openContextMenu(event){
                event&&event.preventDefault();
                event&&event.stopPropagation();
                this.$refs.context.openMenu(event)
            },
            handleSelect(value){
                console.info("select item ",value)
            }
        }
    }
</script>
<style>

</style>
