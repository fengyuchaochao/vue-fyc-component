<template>
    <button @click="handleClick">
        <slot></slot>
    </button>
</template>

<script>
export default {
    name: 'FycButton',
    data () {
        return {

        };
    },
    methods: {
        handleClick (event) {
            this.$emit('click', event);
            event.preventDefault();
        }
    }
}
</script>
