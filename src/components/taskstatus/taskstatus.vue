<template>
    <div class="ivu-taskstatus" v-transfer-dom :data-transfer="transfer">
        <transition name="ease" >
            <div :class="itemClasses">
                <div :class="headerClasses" >
                    <slot name="title"></slot>
                    <Tooltip :content="statusTitle" placement="bottom" class="transfer">
                        <i-button  type="dashed" shape="circle" icon="chevron-up"
                                 size="small" style="border:none;color:white;" @click="toggle()">
                        </i-button>
                    </Tooltip>
                    <Tooltip content="关闭" placement="bottom" class="close">
                        <i-button  type="dashed" shape="circle" icon="close-round" size="small"
                                 style="border:none;color:white;" @click="close">
                        </i-button>
                    </Tooltip>
                </div>
                <collapse-transition>
                    <div :class="contentClasses" v-show="isActive">
                        <div :class="boxClasses"><slot name="content"></slot></div>
                    </div>
                </collapse-transition>
            </div>
        </transition>
    </div>

</template>
<script>
    import Icon from '../icon/icon.vue';
    import Tooltip from '../tooltip/tooltip.vue'
    import iButton from '../button/button.vue';
    import TransferDom from '../../directives/transfer-dom';
    import CollapseTransition from '../base/collapse-transition';
    const prefixCls = 'ivu-taskstatus';

    export default {
        name: 'taskstatus',
        directives: { TransferDom },
        components: { Icon, CollapseTransition,Tooltip,iButton},
        props: {
            transfer:{
                type:Boolean,
                default:true
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
            toggle (val) {
                if(val==undefined){
                    this.isActive = !this.isActive;
                }else{
                    this.isActive = val;
                }
                this.$emit('openDetail', this.isActive);
            },
            close(){
                this.$emit('close', this.isActive);
            }
        }
    };
</script>
