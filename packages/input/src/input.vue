<template>
    <input v-bind="$attrs" :type="type" :value="value" @input="handleInput">
</template>

<script>
export default {
    name: 'FycInput',
    inheritAttrs: false,
    props: {
        type: {
            type: String,
            default: 'text'
        },
        value: {
            type: String
        }
    },
    data () {
        return {

        };
    },
    methods: {
        handleInput (event) {
            this.$emit('input', event.target.value);
            const findParent = parent => {
                while (parent) {
                    if (parent.$options.name === 'FycFormItem') {
                        break;
                    } else {
                        parent = parent.$parent;
                    }
                }
                return parent;
            };
            const parent = findParent(this.$parent);
            if (parent) {
                parent.$emit('validate')
            }
        }
    }
}
</script>
