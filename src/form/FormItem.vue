<template>
    <div>
        <label>{{label}}</label>
        <div>
            <slot></slot>
            <p>{{errorMessage}}</p>
        </div>
    </div>
</template>

<script>
    import AsyncValidator from 'async-validator';
    export default {
        name: 'FycFormItem',
        inject: ['form'],
        props: {
            label: {
                type: String
            },
            prop: {
                type: String
            }
        },
        data () {
            return {
                errorMessage: ''
            }
        },
        methods: {
            validate () {
                if (!this.prop) {
                    return;
                }
                const value = this.form.model[this.prop];
                const rules = this.form.rules[this.prop];

                const data = {
                    [this.prop]: value
                };
                const descriptor = {
                    [this.prop]: rules
                };
                const validator = new AsyncValidator((descriptor));
                return validator.validate(data, (error) => {
                    if (error) {
                        this.errorMessage = error[0].message
                    } else {
                        this.errorMessage = '';
                    }
                })

            }
        },
        mounted () {
            this.$on('validate', () => {
                this.validate();
            })
        }
    }
</script>
