<template>
  <el-dialog title="新增信息" :visible.sync="dialogFormVisible" :before-close="cancel">
    <el-form :model="newdata">
      <el-form-item label="ID" :label-width="formLabelWidth">
        <el-input style="width: 300px" v-model="newdata.contactId" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item label="姓名" :label-width="formLabelWidth">
        <el-input style="width: 300px" v-model="newdata.contactName" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item label="手机号" :label-width="formLabelWidth">
        <el-input style="width: 300px" v-model="newdata.contactPhone" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item label="生日" :label-width="formLabelWidth">
        <el-date-picker
          v-model="newdata.contactBirthday"
          type="date"
          style="width: 300px"
          format="yyyy-MM-dd"
          value-format="yyyy-MM-dd"
          placeholder="选择生日时间">
        </el-date-picker>
      </el-form-item>
      <el-form-item label="性别" :label-width="formLabelWidth">
        <el-select v-model="newdata.sex" placeholder="请选择性别" style="width: 300px">
          <el-option label="男" value="男"></el-option>
          <el-option label="女" value="女"></el-option>
        </el-select>
      </el-form-item>
    </el-form>
    <div slot="footer" class="dialog-footer">
      <el-button @click="cancel">取 消</el-button>
      <el-button type="primary" @click="add">确 定</el-button>
    </div>
  </el-dialog>
</template>

<script>
import axios from 'axios'

export default {
  name: 'AddInfo',
  props: ['formLabelWidth', 'visible'],
  data () {
    return {
      dialogFormVisible: false,
      newdata: {
        contactId: null,
        contactName: '',
        contactPhone: '',
        contactBirthday: '',
        sex: ''
      }
    }
  },
  methods: {
    cancel (done) {
      this.$emit('cancel')
      if (done) {
        done()
      }
    },
    add () {
      this.$emit('cancel')
      axios.post('http://101.34.24.163:8081/contact', JSON.stringify(this.newdata), {
        headers: {
          'Content-Type': 'application/json'
        }
      }).then(() => {
        this.$emit('refresh')
      })
    }
  },
  watch: {
    visible (news) {
      this.dialogFormVisible = news
    }
  },
  created () {
    this.dialogFormVisible = this.visible
  }
}
</script>

<style scoped>

</style>
