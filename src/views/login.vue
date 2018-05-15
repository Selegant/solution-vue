<template>
        <div id="login" class="login">
            <div class="login-con">
                <Card :bordered="false">
                    <p slot="title">
                        <Icon type="log-in"></Icon>
                        欢迎登录
                    </p>
                    <div class="form-con">
                        <Form ref="loginForm" :model="form" :rules="rules">
                            <FormItem prop="userName">
                                <Input v-model="form.userName" placeholder="请输入用户名"/><span slot="prepend"><Icon
                                :size="16"
                                type="person"></Icon></span>
                            </FormItem>
                            <FormItem prop="password">
                                <Input type="password" v-model="form.password" placeholder="请输入密码"/><span
                                slot="prepend"><Icon
                                :size="14" type="locked"></Icon></span>
                            </FormItem>
                            <FormItem>
                                <Button type="primary"  class="button">登录</Button>
                                <Button type="primary"  class="button">注册</Button>
                            </FormItem>
                        </Form>
                    </div>
                </Card>
            </div>
        </div>
</template>

<script>
export default {
    data () {
        return {
            form: {
                userName: '',
                password: ''
            },
            rules: {
                userName: [
                    {required: true, message: '账号不能为空', trigger: 'blur'}
                ],
                password: [
                    {required: true, message: '密码不能为空', trigger: 'blur'}
                ]
            }
        }
    }
}
</script>

<style scoped>
    .login {
        width: 20%;
        height: 20%;
        position: relative;
        margin: 15% auto;
    }
    .form-con{
        padding: 10px 0 0;
    }
    .login-tip{
        font-size: 10px;
        text-align: center;
        color: #c3c3c3;
    }
    .button{
        margin: 2%;
        width: 45%;
    }
</style>
