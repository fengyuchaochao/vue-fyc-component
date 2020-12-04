<template>
    <div>
        <h1>自定义组件</h1>
        <div>
            <FycForm ref="fycForm" :model="user" :rules="formRules">
                <FycFormItem label="用户名" prop="username">
                    <FycInput v-model="user.username" placeholder="请输入用户名" required/>
                </FycFormItem>
                <FycFormItem label="密码" prop="password">
                    <FycInput v-model="user.password" type="password" placeholder="请输入密码" required/>
                </FycFormItem>

            </FycForm>
            <FycButton @click="login">登录</FycButton>
        </div>
    </div>
</template>
<script>
import FycForm from './src/form/Form';
import FycFormItem from './src/form/FormItem';
import FycInput from './src/form/Input';
import FycButton from './src/form/Button';
export default {
    name: 'app',
    components: {
        FycForm,
        FycFormItem,
        FycInput,
        FycButton
    },
    data () {
        return {
            user: {
                username: '',
                password: ''
            },
            formRules: {
                username: {
                    required: true
                },
                password: {
                    required: true
                }
            }
        }
    },
    methods: {
        login () {
            console.log('登录')
            this.$refs['fycForm'].validate(valid => {
                console.log(valid)
            })
        }
    }
}
</script>
<style>

</style>
