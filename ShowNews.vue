<template>
    <div>
        <table>
            <tr>
                <td>id</td>
                <td>名称</td>
                <td>描述</td>
                <td>邮箱</td>
                <td>图片</td>
                <td>操作</td>
            </tr>
            <tr v-for="item in data">
                <td>{{item.id}}</td>
              <td>{{item.name}}</td>
                <td>{{item.desc}}</td>
                <td>{{item.emali}}</td>
                <td><img :src="item.img" style="width: 20px;height: 20px;"></td>
                <td><button @click="del(item.id)">删除</button></td>
                <td><router-link :to="'NewList'+item.id">修改</router-link></td>
            </tr>
        </table>
    </div>
</template>

<script>
    export default {
        name: "ShowNews",
        data(){
            return{
                data:'',
                id:''
            }
        },
        created:function() {
            var _this=this;
            this.$axios.get('/api/api/login')
                .then(function (response) {
                    console.log(response)
                    _this.data=response.data
                })
                .catch(function (error) {
                    console.log(error);
                });
        },
        methods:{
            del:function (id) {
                var _this=this;
                this.$axios.get('/api/api/del?id='+id)
                    .then(function (response) {
                        console.log(response)
                        _this.data=response.data
                    })
                    .catch(function (error) {
                        console.log(error);
                    });
            }
        }

    }
</script>

