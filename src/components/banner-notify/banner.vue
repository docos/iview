<template>
    <transition name="fade">
        <div v-if="!closed" :class="wrapClasses" @click="click">
            <span :class="iconClasses" v-if="showIcon">
                <slot name="icon">
                    <Icon :type="iconType"></Icon>
                </slot>
            </span>
            <span :class="messageClasses"><slot></slot></span>
            <a :class="closeClasses" v-if="closable" @click="close">
                <slot name="close">
                    <Icon type="ios-close-empty"></Icon>
                </slot>
            </a>
        </div>
    </transition>
</template>
<script>
    import Icon from '../icon';
    import { oneOf } from '../../utils/assist';

    const prefixCls = 'ivu-banner-notify';

    export default {
        name: 'bannerNofity',
        components: { Icon },
        props: {
            type: {
                validator (value) {
                    return oneOf(value, ['success', 'info', 'warning', 'error']);
                },
                default: 'info'
            },
            closable: {
                type: Boolean,
                default: false
            },
            showIcon: {
                type: Boolean,
                default: false
            }
        },
        data () {
            return {
                closed: false,
                desc: false
            };
        },
        computed: {
            wrapClasses () {
                return [
                    `${prefixCls}`,
                    `${prefixCls}-${this.type}`,
                    `${prefixCls}-with-banner`,
                    {
                        [`${prefixCls}-with-icon`]: this.showIcon,
                    }
                ];
            },
            messageClasses () {
                return `${prefixCls}-message`;
            },
            closeClasses () {
                return `${prefixCls}-close`;
            },
            iconClasses () {
                return `${prefixCls}-icon`;
            },
            iconType () {
                let type = '';

                switch (this.type) {
                    case 'success':
                        type = 'checkmark-circled';
                        break;
                    case 'info':
                        type = 'information-circled';
                        break;
                    case 'warning':
                        type = 'android-alert';
                        break;
                    case 'error':
                        type = 'close-circled';
                        break;
                }

                return type;
            }
        },
        methods: {
            close (e) {
                this.closed = true;
                this.$emit('on-close', e);
            },
            click(e){
                this.$emit('click',e);
            },
            open(){
                this.closed = false;
            }
        },
        mounted () {
            this.desc = this.$slots.desc !== undefined;
        }
    };
</script>
