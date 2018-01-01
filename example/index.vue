<template>
  <div>
    <div class="p-10">
      <div class="tc m-b-20 dib">
        <div>
          <figure v-for="(thumbnail, index) in thumbnails" class="dib pos-rel">
            <img :src="`${thumbnail}?imageView2/1/w/100/h/100/interlace/0/q/100`"
                 class="rounded bd-blue m-r-5"/>
            <i class="fa fa-trash btn_remove" @click="deleteFile(index)"></i>
          </figure>
        </div>
      </div>
      <QiniuUpload :multiple="true" @complete="uploadComplete" ref="qiniuUpload" class="l">
        <a></a>
      </QiniuUpload>
    </div>
  </div>
</template>
<script type="text/babel">
  import QiniuUpload from '../qiniuUpload.vue'

  export default{
    components: {
      QiniuUpload,
    },
    data() {
      return {
        thumbnails: [],
      }
    },
    methods: {
      deleteFile(index) {
        this.thumbnails.splice(index, 1)
      },
      uploadComplete(status, result) {
        if (status === 200) {
          this.thumbnails.push(`http://img.hidoge.cn/${result.key}`)
        } else {
          console.log('出错', status)
        }
      },
    },
  }
</script>
<style scoped>
  @import "~font-awesome/css/font-awesome.min.css";

  .pos-rel{
    position: relative;
  }
  .dib {
    display: inline-block;
  }
  .tc {
    text-align: center;
  }
  .p-10 {
    padding: 10px;
  }
  .btn_remove{
    position: absolute;
    right: 10px;
    top: 10px;
    z-index: 1;
    color: #ff0000;
    font-size: 18px;
  }
</style>