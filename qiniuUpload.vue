<template>
  <div class="tc">
    <label class="qiniu-upload tc">
      <div class="spin-auto auto p-t-20" v-if="ing">
        <i class="fa fa-spinner fa-spin c-g9"></i>
      </div>
      <div v-else>
        <div class="p-10">
          <div class="p-t-5"></div>
          <i class="fa fa-plus-circle fa-4x c-blue"></i>
        </div>
        <em>选择图片</em>
        <input id="files" type="file" :accept="accepts" @change="upload" :multiple="multiple">
        <slot></slot>
      </div>
    </label>
  </div>
</template>
<script>
  import axios from 'axios'
  import Config from 'argument.config'

  export default {
    props: {
      accepts: {
        type: String,
        default: 'image/jpeg,image/jpg,image/png,image/gif',
      },
      multiple: [Boolean],
      maxSize: {
        type: Number,
        default: 0,
      },
    },
    data() {
      return {
        file: null,
        ing: false,
        token: null,
      }
    },
    methods: {
      upload(event) {
        const file = event.target.files
        if (file) {
          if (this.maxSize) {
            // todo filter file
          }
          this.ing = true
          axios.get(Config.qiniuTokenApi).then((token) => {
            this.token = token
            _(file).forEach((item) => {
              const formData = new FormData()
              formData.append('file', item)
              formData.append('token', this.token)
              axios.post(Config.qiniuServer, formData).then((response) => {
                const result = response.data
                if (result.hash && result.key) {
                  this.ing = false
                  this.$emit('complete', 200, result)
                } else {
                  this.ing = false
                  this.$emit('complete', 500, result)
                }
              }).catch((err) => {
                console.log('err', err)
              })
            })
          }).catch((err) => {
            console.log('err', err)
          })
        }
      },
    },
  }
</script>
<style scoped>
  @import "~font-awesome/css/font-awesome.min.css";
  .c-g9 {
    color: #999;
  }
  .tc {
    text-align: center;
  }
  .p-10 {
    padding: 10px;
  }
  .p-t-5 {
    padding-top: 5px;
  }
  .qiniu-upload {
    display:block;
    width: 102px;
    height:102px;
    margin: 0 auto;
    border-radius: 10px;
    border:2px dashed #ddd;
    overflow: hidden;
    cursor: pointer;
  }
  .qiniu-upload input[type="file"]{
    display: none;
  }
  .qiniu-upload em{
    font-style: normal;
    text-align: center;
    display:block;
  }
  .spin-auto{
    width: 102px;
    height: 102px;
    position: relative;
  }
</style>