<template>
    <div class="ivu-taskstatus">
        <div :class="itemClasses">
            <div :class="headerClasses" >
                <slot name="title"></slot>
                <Tooltip :content="statusTitle" placement="bottom" class="transfer">
                    <Button  type="dashed" shape="circle" icon="chevron-right"
                             size="small" style="border:none;color:white;" @click="toggle">
                    </Button>
                </Tooltip>
                <Tooltip content="关闭" placement="bottom" class="close">
                    <Button  type="dashed" shape="circle" icon="close-round" size="small"
                             style="border:none;color:white;" @click="close">
                    </Button>
                </Tooltip>
            </div>

            <collapse-transition>
                <div :class="contentClasses" v-show="isActive">
                    <div :class="boxClasses"><slot name="content"></slot></div>
                </div>
            </collapse-transition>
        </div>
    </div>

</template>
<script>
    import Icon from '../icon/icon.vue';
    import Tooltip from '../tooltip/tooltip.vue'
    import Button from '../button/button.vue';
    import CollapseTransition from '../base/collapse-transition';
    const prefixCls = 'ivu-taskstatus';

    export default {
        name: 'taskstatus',
        components: { Icon, CollapseTransition,Tooltip,Button },
        props: {
            name: {
                type: String
            }
        },
        data () {
            return {
                index: 0, // use index for default when name is null
                isActive: false
            };
        },
        computed: {
            itemClasses () {
                return [
                    `${prefixCls}-item`,
                    {
                        [`${prefixCls}-item-active`]: this.isActive
                    }
                ];
            },
            headerClasses () {
                return `${prefixCls}-header`;
            },
            contentClasses () {
                return `${prefixCls}-content`;
            },
            boxClasses () {
                return `${prefixCls}-content-box`;
            },
            statusTitle(){
                if(this.isActive){
                    return "最小化"
                }else{
                    return "最大化"
                }
            }
        },
        methods: {
            toggle () {
                this.isActive = !this.isActive;
                this.$emit('openDetail', this.isActive);
            },
            close(){
                this.$emit('close', this.isActive);
            }
        }
    };
</script>
