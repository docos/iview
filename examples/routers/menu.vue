<template>
    <div>
        <Menu :theme="theme3" active-name="1">
            <MenuGroup title="内容管理">
                <MenuItem name="1">
                    <Icon type="document-text"></Icon>
                    文章管理
                </MenuItem>
                <MenuItem name="2">
                    <Icon type="chatbubbles"></Icon>
                    评论管理
                </MenuItem>
            </MenuGroup>
            <MenuGroup title="统计分析">
                <MenuItem name="3">
                    <Icon type="heart"></Icon>
                    用户留存
                </MenuItem>
                <MenuItem name="4">
                    <Icon type="heart-broken"></Icon>
                    流失用户
                </MenuItem>
            </MenuGroup>
        </Menu>
        <br>
        <p>切换主题</p>
        <Radio-group v-model="theme3">
            <Radio label="light"></Radio>
            <Radio label="dark"></Radio>
            <Radio label="primary"></Radio>
        </Radio-group>
    </div>
</template>
<script>
    export default {
        data () {
            return {
                theme3: 'light'
            }
        }
    }
</script>
