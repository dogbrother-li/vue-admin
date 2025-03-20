<!-- eslint-disable @typescript-eslint/no-unused-vars -->
<script setup lang="ts">
import { ref, computed, reactive } from 'vue'
import { type FormInstance, ElMessage } from 'element-plus'
import { useRouter } from 'vue-router'

const router = useRouter()

// 表单实例
const formRef = ref<FormInstance>()

// 数组类型 const domains = DomainItem[]
interface DomainItem {
  key: number
  value: string
}
// form 表单对象
const dynamicValidateForm = reactive<{
  password: string
  account: string
}>({
  password: '',
  account: '',
})

// 表单校验规则
const rules = ref({
  // account: [
  //   { required: true, message: '手机号不能为空', trigger: 'blur' },
  //   { pattern: /^1[3-9]\d{9}$/, message: '请输入有效的手机号', trigger: 'blur' },
  // ],
})

// 表单提交
const submitForm = (formEl: FormInstance | undefined) => {
  const account = dynamicValidateForm.account
  const password = dynamicValidateForm.password
  if (!formEl) return
  formEl.validate((valid) => {
    if (valid) {
      console.log(account, password, 'submit!')
      if (account === 'admin' && password === '123') {
        console.log('登录成功')
        dynamicValidateForm.account = ''
        dynamicValidateForm.password = ''
        router.push('/home')
      } else {
        console.log('登录失败')
        ElMessage.error('登录失败')
        dynamicValidateForm.account = ''
        dynamicValidateForm.password = ''
      }
    } else {
      console.log('error submit!')
    }
  })
}

// 重置表单
const resetForm = (formEl: FormInstance | undefined) => {
  if (!formEl) return
  formEl.resetFields()
}
</script>

<template>
  <!-- <header>
    <div class="wrapper">
      <button @click="increment">
      </button>
      <el-button type="primary">Primary</el-button>
    </div>
  </header> -->

  <div class="wrapper">
    <el-form
      ref="formRef"
      style="max-width: 600px"
      :model="dynamicValidateForm"
      :rules="rules"
      label-width="auto"
      class="demo-dynamic"
    >
      <h2 class="formTitle">登录表单</h2>

      <!-- 账号输入框 -->
      <el-form-item
        prop="account"
        label="账号"
        :rules="[
          // {
          //   type: 'email',
          //   message: 'Please input correct email address',
          //   trigger: ['blur', 'change'],
          // },
          {
            required: true,
            message: '账号不能为空',
            trigger: 'blur',
          },
        ]"
      >
        <el-input v-model="dynamicValidateForm.account" clearable placeholder="请输入账号" />
      </el-form-item>

      <!-- 密码输入框 -->
      <el-form-item
        prop="password"
        label="密码"
        :rules="{
          required: true,
          message: '密码不能为空',
          trigger: 'blur',
        }"
      >
        <el-input
          v-model="dynamicValidateForm.password"
          show-password
          clearable
          placeholder="请输入密码"
          @keyup.enter="submitForm(formRef)"
        />
      </el-form-item>

      <!-- 提交按钮 -->
      <el-form-item>
        <el-button type="primary" @click="submitForm(formRef)">登录</el-button>
        <el-button @click="resetForm(formRef)">取消</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<style scoped>
@media (min-width: 1024px) {
  .wrapper {
    height: 100%;
    box-sizing: border-box;
    overflow: hidden;
    background-color: #eff0f4;
  }
  .formTitle {
    margin-bottom: 15px;
  }
  .demo-dynamic {
    max-width: 800px;
    height: 270px;
    padding: 15px;
    margin-top: 15%;
    margin-left: 25%;
    background-color: #fff;
  }
  /* header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  } */
}
</style>
