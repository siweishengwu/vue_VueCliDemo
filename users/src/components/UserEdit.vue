<template>
    <div>
        <h2>编辑用户信息</h2>
        <form action="">
            用户名:<input v-model="user.name" type="text"><br>
            年龄:<input v-model="user.age" type="text"><br>
            生日:<input v-model="user.bir" type="text"><br>
            <input type="button" @click="editUserInfo()" value="修改">
        </form>
    </div>
  </template>

<script>
    export default {
        name: 'UserEdit',
        data() {
            return {
                user: {
                    id: ""
                }
            }
        },
        methods: {
            findOne() {
                this.$http.get("http://rap2.taobao.org:38080/app/mock/265382/user/findOne?id=" + this.user.id).then(res => {
                    console.log(res.data);
                    this.user = res.data;
                });
            },
            editUserInfo() {
                this.$http.post("http://rap2.taobao.org:38080/app/mock/265382/user/update", this.user).then(res => {
                    console.log(res);
                    if (res.data.success) {
                        this.$router.push("/user"); //切换路由
                    }
                });
            }
        },
        created() {
            console.log("修改主键中获取的id" + this.$route.query.id);
            this.user.id = this.$route.query.id;
            this.findOne();
        },
    }
</script>

<style scoped>

</style>