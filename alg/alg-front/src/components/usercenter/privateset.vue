<template>
   <div class="adatar">
        <!--三元表达式，如果有默认头像，显示默认头像，如果没有，显示本地图片-->
        <img :src="adatar?adatar:require('../../assets/touxiang.gif')" alt="" >
        <!--文件上传-->
        <input type="file" name="" accept="image/gif,image/jpeg,image/jpg,image/png" @change="fileChange">
        <!--文件提交-->
        <button @click="submit">提交</button>
    </div>
</template>

<script>
export default {
  name: 'adatar',
    data() {
        return {
            adatar: ''
        }
    },
    methods: {
        //头像选择
        fileChange(e) {
            var that = this;
            var file = e.target.files[0];
            var reader = new FileReader();
            reader.onload = function(e){
                that.adatar  = e.target.result;
            }
            reader.readAsDataURL(file);
        },
        submit() {
            var data = new FormData();
            data.appendTo('file',this.adatar);
            $ajax({
                type: 'POST',
                data: data,
                processData: false, //processData 默认为false，当设置为true的时候,jquery ajax 提交的时候不会序列化 data，而是直接使用data
                contentType: false,
                success:function(res){
                },
                error:function(err){
                }
            })
        }
    }
}
</script>

<style lang="less">
    .adatar {
        position: relative;
        width: 168px;
        height: 168px;
        img {
            object-fit: cover;
            object-position: center;
            width: 100%;
            height: 100%;
            border-radius: 50%;
        }
        input {
            position: absolute;
            top: 0;
            right: 0;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            outline: none;
            opacity: 0;
            cursor: pointer;
            &:focus {
                box-shadow: none;
            }
        }
        button {
            width: 100%;
            height: 30px;
            margin-top: 20px;
            text-align: center;
            border: 1px solid #ccc;
            color: #fff;
            font-size: 14px;
            background: pink;
        }

    }
</style>