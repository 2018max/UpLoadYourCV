
<template>
  <v-slot name="header">
    <div class="logo"  >
      <img src="./assets/vue.svg" alt="logo" class="vue" style="width: 200rem; height: 200rem; max-width: 100%; max-height: 100%; margin-top: 3rem;" justify="center"   />
    </div>
  </v-slot>
  <el-row :gutter="10">
    <el-col :xs="8" :sm="6" :md="4" :lg="3" :xl="1">
      <div class="grid-content ep-bg-purple" />
    </el-col>
    <el-col :xs="4" :sm="6" :md="8" :lg="9" :xl="11">
      <div class="grid-content ep-bg-purple-light" />
    </el-col>
    <el-col :xs="4" :sm="6" :md="8" :lg="9" :xl="11">
      <div class="grid-content ep-bg-purple" />
    </el-col>
    <el-col :xs="8" :sm="6" :md="4" :lg="3" :xl="1">
      <div class="grid-content ep-bg-purple-light" />
    </el-col>
  </el-row>
<div class="itemClass"    >
  <el-row :gutter="10"  justify="center" style="margin-top: 20px;">
      <el-col :xs="8" :sm="6" :md="4" :lg="3" :xl="1">
        <el-input
          v-model="account"
          style="width: 15rem; "
          placeholder="请输入邮箱"
          @blur="validateEmail"
        />
        <el-alert
      v-if="emailError"
      :title="emailError"
      type="error"
      style="margin-top: 10px;"
    />
      </el-col>
  </el-row>
  <el-row :gutter="10" style="margin-top: 20px;" justify="center">
      <el-col :xs="8" :sm="6" :md="4" :lg="3" :xl="1" >
        <el-input
          v-model="password"
          class="custom-input"
          style="width: 15rem; "
          type="password"
          @focus="handleFoucs"
           @blur="validatePassword"
          placeholder="请输入密码"
          show-password
        />
        <el-alert
      v-if="passwordError"
      :title="passwordError"
      type="error"
      style="margin-top: 10px;"
    />
      </el-col>
    </el-row>
    <el-alert
      v-if="errorMessage"
      :title="errorMessage"
      type="error"
      style="margin-top: 10px;"
    />
    <el-row :gutter="10" style="margin-top: 20px;"justify="center">
      <el-col :xs="8" :sm="6" :md="4" :lg="3" :xl="1" >
        <el-button 
        style="width: 6rem;"
        class="custom-button"
          type="success" 
          :loading="loading" 
          @click="login">
          登录
        </el-button>
      </el-col>
      </el-row>
    <el-row :gutter="10" style="margin-top: 20px;" justify="center">
      <el-col :xs="8" :sm="6" :md="4" :lg="3" :xl="1" >
        <el-button type="primary" style="width: 6rem;">忘记密码？</el-button>
      </el-col>
    </el-row>
</div>



 
</template>

<script setup lang="ts">
import { ref } from 'vue'
const account = ref('');
const password = ref('');
const loading = ref(false);
const errorMessage = ref('');
const emailError = ref('');
const passwordError = ref('');
const handleFoucs = () => {
  console.log('handleFoucs');
  }
const validatePassword = () => {
      if (password.value.length < 6) {
        passwordError.value = '密码长度至少为 6 个字符';
      } else {
        passwordError.value = ''; // 清空错误信息
      }
    };

const validateEmail = () => {
      // 邮箱的正则表达式
      const emailPattern = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      if (!emailPattern.test(account.value)) {
        emailError.value = '请输入有效的邮箱地址';
      } else {
        emailError.value = ''; // 清空错误信息
      }
    };

const login = () => {
  loading.value = true; // 开始加载
  errorMessage.value = ''; // 清空错误提示

  // 模拟一个网络请求
  setTimeout(() => {
    if (account.value === '' || password.value === '') {
      errorMessage.value = '账号和密码不能为空'; // 设置错误提示
    } else if (account.value !== 'admin' || password.value !== '123456') {
      errorMessage.value = '账号或密码错误'; // 设置错误提示
    } else {
      console.log("登录成功");
      // 处理登录成功后的逻辑
    }
    loading.value = false; // 结束加载
  }, 2000); // 模拟2秒的请求时间
}
import {  } from '@element-plus/icons-vue'






</script>
<style scoped>
.custom-input {
  transition: border 0.3s ease, box-shadow 0.3s ease; /* 添加过渡效果 */
}

/* 聚焦效果 */
.custom-input .el-input__inner:focus {
  border-color: #409eff; /* 聚焦时边框颜色 */
  box-shadow: 0 0 5px rgba(64, 158, 255, 0.5); /* 聚焦时阴影效果 */
}
.custom-button {
  transition: background-color 0.3s ease, color 0.3s ease; /* 添加过渡效果 */
}

.custom-button:hover {
  background-color: #6ab04c; /* 悬浮时背景颜色 */
  color: white; /* 悬浮时字体颜色 */
}

.custom-button:focus {
  outline: none; /* 去除聚焦时的边框 */
}
.el-col {
  border-radius: 4px;
}

.grid-content {
  border-radius: 4px;
  min-height: 36px;
}
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
