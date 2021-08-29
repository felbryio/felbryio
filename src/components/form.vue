<template>
  <div>
    <el-form
      v-for="(form, formIndex) in formList"
      :key="form.title"
      label-width="auto"
    >
      <el-form-item :label="`${formIndex + 1}、`">
        <el-input v-model="form.title" />
        <el-button
          v-if="formIndex === formList.length - 1"
          icon="el-icon-plus"
          circle
          @click="addForm"
        />
        <el-button
          v-if="formIndex > 0"
          icon="el-icon-minus"
          circle
          @click="delForm(formIndex)"
        />
      </el-form-item>
      <el-form-item>
        <el-form label-width="auto">
          <el-form-item
            v-for="(item, index) in form.list"
            :key="index"
            :label="`${index + 1}）`"
          >
            <el-input
              v-model="item.content"
              type="textarea"
              autosize
              :placeholder="`工作内容${index + 1}`"
            />
            <el-input
              v-model="item.progress"
              placeholder="进度"
            >
              <template slot="append">
                %
              </template>
            </el-input>
            <el-button
              icon="el-icon-plus"
              circle
              @click="addItem(form.list, index)"
            />
            <el-button
              v-if="index > 0"
              icon="el-icon-minus"
              circle
              @click="delItem(form.list, index)"
            />
          </el-form-item>
        </el-form>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
class Item {
  constructor () {
    this.content = ''
    this.progress = ''
  }
}
class Form {
  constructor () {
    this.title = ''
    this.list = [
      new Item()
    ]
  }
}
export default {
  data () {
    return {
      formList: [new Form()]
    }
  },
  methods: {
    addForm () {
      this.formList.push(new Form())
    },
    delForm (index) {
      this.formList.splice(index, 1)
    },
    addItem (list, index) {
      list.splice(index + 1, 0, new Item())
    },
    delItem (list, index) {
      list.splice(index, 1)
    }
  }
}
</script>

<style lang="less" scoped>
/deep/ .el-form-item__content {
  display: flex;
}
</style>
