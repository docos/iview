<template>
    <div style="width: 400px;margin: 200px;">
        <TaskStatus name="1">
            史蒂夫·乔布斯
            <p slot="content">史蒂夫·乔布斯（Steve Jobs），1955年2月24日生于美国加利福尼亚州旧金山，美国发明家、企业家、美国苹果公司联合创办人。</p>
        </TaskStatus>
    </div>
</template>
<script>
    export default {
        props: {},
        data () {
            return {
                v1: '2'
            };
        },
        computed: {},
        methods: {}
    };
</script>