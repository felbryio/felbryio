<template>
  <div>
    <el-card>
      写周报步骤：<br>
      1. 填写表单<br>
      2. 填写姓名并下载Word附件<br>
      3. 打开邮箱地址 http://mail.chinatelecom.cn/webmail/signOn.do，新建邮件，并将 邮件标题 和 Word全部内容 复制粘贴进邮件<br>
      4. 确认 收件人和抄送人 点击发送
    </el-card>
    <h1>一、本周完成重点工作</h1>
    <MyForm ref="currentJob" />
    <h1>二、下周重点工作</h1>
    <MyForm ref="nextJob" />
    <h1>三、意见建议</h1>
    <el-input
      v-model="form.suggestion"
      type="textarea"
      autosize
      placeholder="意见建议"
    />
    <h1>四、培训需求</h1>
    <el-input
      v-model="form.train"
      type="textarea"
      autosize
      placeholder="培训需求"
    />
    <h1>五、待解决问题</h1>
    <el-input
      v-model="form.unresolved"
      type="textarea"
      autosize
      placeholder="待解决问题"
    />
    <el-divider />
    <el-card>
      <el-form label-width="auto">
        <el-form-item label="你的姓名：">
          <el-input v-model="name" />
        </el-form-item>
        <el-form-item label="标准邮件标题（输入姓名后复制）：">
          {{ name }}-周报-{{ startDay }}_{{ endDay }}
        </el-form-item>
      </el-form>
    </el-card>
    <el-button
      type="primary"
      style="margin-top: 20px"
      @click="$emit('down')"
    >
      下载Word附件
    </el-button>
  </div>
</template>

<script>
import MyForm from '@/components/form.vue'
class Form {
  constructor () {
    this.suggestion = ''
    this.train = ''
    this.unresolved = ''
  }
}
export default {
  components: {
    MyForm
  },
  data () {
    return {
      // eslint-disable-next-line
      startDay: dayjs().startOf('week').add(1, 'day').format('YYYY-MM-DD'),
      // eslint-disable-next-line
      endDay: dayjs().endOf('week').subtract(1, 'day').format('YYYY-MM-DD'),
      name: '',
      form: new Form()
    }
  },
  methods: {
    getData () {
      return {
        name: this.name,
        ...this.form,
        currentJob: this.$refs.currentJob.formList,
        nextJob: this.$refs.nextJob.formList
      }
    }
  }
}
</script>

<style>

</style>
