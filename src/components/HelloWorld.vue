<template>
  <div class="hello">
    <el-upload class="avatar-uploader" action="https://jsonplaceholder.typicode.com/posts/" :on-success="handleAvatarSuccess" :before-upload="beforeAvatarUpload" :on-preview="handlePreview" :on-remove="handleRemove" :file-list="fileList" :auto-upload="false">
      <el-button slot="trigger" size="small" type="primary">选取文件</el-button>
      <el-button style="margin-left: 10px;" size="small" type="success" @click="submitUpload">上传到服务器</el-button>
      <img v-if="imageUrl" :src="imageUrl" class="avatar">
      <i v-else class="el-icon-plus avatar-uploader-icon"></i>
    </el-upload>
  </div>
</template>

<script>
export default {
    data() {
        return {
            imageUrl: "",
            fileList: [
                {
                    name: "food.jpeg",
                    url:
                        "https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100"
                },
                {
                    name: "food2.jpeg",
                    url:
                        "https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100"
                }
            ]
        };
    },
    methods: {
        submitUpload() {
            this.$refs.upload.submit();
        },
        handleRemove(file, fileList) {
            console.log(file, fileList);
        },
        handlePreview(file) {
            console.log(file);
        },
        handleAvatarSuccess(res, file) {
            this.imageUrl = URL.createObjectURL(file.raw);
        },
        beforeAvatarUpload(file) {
            // 文件限制
            const isFile =
                (file.type === "image/jpeg") |
                (file.type === "image/png") |
                (file.type === "image/gif") |
                (file.type === "image/jpg") |
                (file.type === "application/vnd.ms-powerpoint") |
                (file.type === "application/x-ppt") |
                (file.type === "application/x-xls") |
                (file.type === "application/vnd.ms-excel") |
                (file.type === "application/msword") |
                (file.type === "text/plain") |
                (file.type === "application/pdf") |
                (file.type === "text/html") |
                (file.type === "text/html") |
                (file.type === "application/vnd.rn-realmedia-vbr") |
                (file.type === "video/avi") |
                (file.type === "audio/x-ms-wma") |
                (file.type === "audio/wav") |
                (file.type === "audio/mp3") |
                (file.type === "video/mpeg4");
            // 大小限制
            const isLt2M = file.size / 1024 / 1024 < 2;

            if (!isFile) {
                this.$message.error("上传的文件格式不符合要求!");
            }
            if (!isLt2M) {
                this.$message.error("上传头像图片大小不能超过 2MB!");
            }
            return isFile && isLt2M;
        }
    }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.avatar-uploader .el-upload {
    border: 1px dashed #d9d9d9;
    border-radius: 6px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
}
.avatar-uploader .el-upload:hover {
    border-color: #409eff;
}
.avatar-uploader-icon {
    font-size: 28px;
    color: #8c939d;
    width: 178px;
    height: 178px;
    line-height: 178px;
    text-align: center;
}
.avatar {
    width: 178px;
    height: 178px;
    display: block;
}
</style>
