<template>
    <div class="dialog" v-if="show" @click.stop="closeDialog">
        <div @click.stop class="dialog__content">
            <slot></slot>
        </div>
    </div>
</template>

<script>
    export default {
        name:'MyDialog',
        props: {
            show: {
                type: Boolean,
                default: false
            }
        },
        methods: {
            closeDialog() {
                this.$emit('update:show', false )
            }
        }
    }
</script>

<style scoped>
    .dialog {
        top:0;
        bottom:0;
        right:0;
        left: 0;
        background: rgba(0,0,0,0.5);
        position: fixed;
        display: flex;
        z-index: 999;
    }

    .dialog__content {
        margin: auto;
        background: #fff;
        border-radius: 30px;
        min-height: 50px;
        min-width: 500px;
        padding:10px
    }
</style> 