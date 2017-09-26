<template>
    <Context :items="items">

    </Context>
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
        methods: {}
    }
</script>
<style>

</style>
