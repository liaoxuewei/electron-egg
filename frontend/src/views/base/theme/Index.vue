<template>
  <div id="app-base-screen">
    <div class="one-block-1">
      <span>
        1. 系统主题模式
      </span>
    </div>
    <div class="one-block-2">
      <a-space>
        <a-button @click="getTheme()">获取模式</a-button>
      </a-space>
      <span>
        结果：{{ currentThemeMode }}
      </span>
    </div>
    <div class="one-block-1">
      2. 设置主题模式（请自行实现前端UI效果）
    </div>  
    <div class="one-block-2">
      <a-radio-group v-model="currentThemeMode" @change="setTheme">
        <a-radio :value="themeList[0]">
          {{ themeList[0] }}
        </a-radio>
        <a-radio :value="themeList[1]">
          {{ themeList[1] }}
        </a-radio>
        <a-radio :value="themeList[2]">
          {{ themeList[2] }}
        </a-radio>
      </a-radio-group>
    </div>
  </div>
</template>
<script>
import { ipcApiRoute } from '@/api/main'

export default {
  data() {
    return {
      currentThemeMode: '',
      themeList: [
        'system',
        'light',
        'dark'
      ]
    };
  },
  mounted () {
  },
  methods: {
    setTheme (e) {
      const self = this;
      this.currentThemeMode = e.target.value;
      console.log('setTheme currentThemeMode:', this.currentThemeMode)

      this.$ipcCall(ipcApiRoute.setTheme, this.currentThemeMode).then(result => {
        console.log('result:', result)
        self.currentThemeMode = result;
      })      
    },
    getTheme () {
      const self = this;
      this.$ipcCall(ipcApiRoute.getTheme).then(result => {
        console.log('result:', result)
        self.currentThemeMode = result;
      })  
    },
  }
};
</script>
<style lang="less" scoped>
#app-base-screen {
  padding: 0px 10px;
  text-align: left;
  width: 100%;
  .one-block-1 {
    font-size: 16px;
    padding-top: 10px;
  }
  .one-block-2 {
    padding-top: 10px;
  }
}
</style>
