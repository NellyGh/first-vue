<template>
    <select :value="modelValue" @change="checkOption" class="select">
        <option  disabled value="">Check from List</option>
        <option v-for="option in options" :key="option.value" :value="option.value">{{ option.name }}</option>
    </select>
</template>

<script>
    export default {
        name: "MySelect",
        props: {
            modelValue: {
                type: String
            },
            options: {
                type: Array,
                default: () => []

            }
        },
        methods: {
            checkOption(event) {
                this.$emit('update:modelValue', event.target.value)

            }
        }
    }
</script>

<style  scoped>
    .select {
        border-radius: 30px;
        background: coral;
        border:none;
        color: #fff

    }

</style>