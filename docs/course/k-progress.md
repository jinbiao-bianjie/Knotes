---
sidebarDepth: 2
---

# 🌈 k-progress

> 一个 Vue 插件，线性进度条。

![](https://img.shields.io/npm/v/k-progress?color=success&style=flat-square)
![](https://img.shields.io/github/languages/top/xrkffgg/k-progress?style=flat-square)
![](https://img.shields.io/github/languages/code-size/xrkffgg/k-progress?color=orange&style=flat-square)
![](https://img.shields.io/github/stars/xrkffgg/k-progress?color=blueviolet&style=flat-square)
![](https://img.shields.io/github/license/xrkffgg/k-progress?color=red&style=flat-square)
![](https://img.shields.io/npm/dt/k-progress?color=ff69b4&style=flat-square)

## 📦 安 装
```bash
# vue2
npm install -S k-progress
# vue3
npm install -S k-progress-v3
# or
yarn add k-progress
yarn add k-progress-v3
```
## 🔨 开始使用
```js
// main.js - vue2
import KProgress from 'k-progress';
Vue.component('k-progress', KProgress);

// main.js - vue3
import KProgress from 'k-progress';

const app = createApp(App);
app
  .component('k-progress', KProgress)
  .mount('#app');
```
## 🌀 例 子
### 🌟 基本用法
> 可设置不同的 `status` 、 `border` 、`color` 、 `bg-color` 展示不同的颜色效果

<demo-code>
  <kprogress-base></kprogress-base>
  <highlight-code slot="codeText" lang="vue">
    <template>
      <div>
        <k-progress :percent="10"></k-progress>
        <k-progress :percent="20" status="success"></k-progress>
        <k-progress :percent="30" status="warning" :border="false"></k-progress>
        <k-progress :percent="40" status="error"></k-progress>
        <k-progress :percent="50" color="#9254de"></k-progress>
        <k-progress :percent="60" :color="['#f5af19', '#f12711', '#9254de', '#40a9ff', '#5cdbd3']" :border="false"></k-progress>
        <k-progress :percent="70" :color="['#40a9ff', '#5cdbd3']" bg-color="#d9f7be"></k-progress>
        <k-progress :percent="percent" :color="getColor"></k-progress>
      </div>
    </template>

    <script>
      export default {
        data: {
          return {
            percent: 10,
            ifUp: true,
          }
        },
        mounted () {
          const timer = setInterval(() =>{
            if (this.ifUp) {
              this.percent = this.percent + 10
              this.percent == 100 ? this.ifUp = false : this.ifUp = true
            } else {
              this.percent = this.percent - 10
              this.percent == 10 ? this.ifUp = true : this.ifUp = false
            }
          }, 1000);
          this.$once('hook:beforeDestroy', () => clearInterval(timer));
        },
        methods: {
          getColor(percent) {
            if(percent < 40){
              return '#ffc069';
            } else if(percent < 60) {
              return '#fadb14';
            } else if(percent < 80) {
              return '#13c2c2';
            } else {
              return '#389e0d';
            }
          }
        },
      }
    </script>
  </highlight-code>
</demo-code>

### 🌟 不同类型
> 可设置 `lump` 类型，同时支持宽度和颜色设置

<demo-code>
  <kprogress-lump></kprogress-lump>
  <highlight-code slot="codeText" lang="vue">
    <template>
      <div>
        <k-progress :percent="20" ></k-progress>
        <k-progress :percent="40" status="success" type="lump" ></k-progress>
        <k-progress :percent="60" status="warning" type="lump" active :border="false" ></k-progress>
        <k-progress :percent="80" :color="['#40a9ff', '#5cdbd3']" type="lump" :cut-width="2" cut-color="#389e0d"></k-progress>
      </div>
    </template>
  </highlight-code>
</demo-code>

### 🌟 高度设置
> 可设置不同的 `line-height` 展示不同的尺寸，默认为 `6` 

<demo-code>
  <kprogress-line-height></kprogress-line-height>
  <highlight-code slot="codeText" lang="vue">
    <template>
      <div>
        <k-progress :percent="10" ></k-progress>
        <k-progress :percent="20" status="success" :line-height="8"></k-progress>
        <k-progress :percent="30" status="warning" :line-height="10"></k-progress>
        <k-progress :percent="40" status="error" :line-height="12"></k-progress>
      </div>
    </template>
  </highlight-code>
</demo-code>

### 🌟 文字设置
> 可通过 `show-text` 设置是否显示文字，可 `format` 自定义文字显示

<demo-code>
  <kprogress-text></kprogress-text>
  <highlight-code slot="codeText" lang="vue">
    <template>
      <div>
        <k-progress :percent="50" ></k-progress>
        <k-progress :percent="60" status="success" :show-text="false" ></k-progress>
        <k-progress :percent="80" status="warning" :format="format"></k-progress>
        <k-progress :percent="100" status="error" :format="format"></k-progress>
      </div>
    </template>

    <script>
      export default {
        methods: {
          format(percent) {
            if(percent == 100){
              return '^_^'
            }
            return 'QAQ'
          }
        },
      }
    </script>
  </highlight-code>
</demo-code>

### 🌟 动效设置
> 可通过 `active` 、 `active-color` 、 `color-flow` 来设置进度条动态效果

<demo-code>
  <kprogress-active></kprogress-active>
  <highlight-code slot="codeText" lang="vue">
    <template>
      <div>
        <k-progress :percent="40" active></k-progress>
        <k-progress :percent="60" active active-color="#f12711"></k-progress>
        <k-progress :percent="80" active :color="['#f5af19', '#f12711', '#9254de', '#40a9ff', '#5cdbd3']"></k-progress>
        <k-progress :percent="100" :color="['#f5af19', '#f12711', '#9254de', '#40a9ff', '#5cdbd3']" :color-flow="true"></k-progress>
      </div>
    </template>
  </highlight-code>
</demo-code>

## 📔 参 数
|    参 数     |           类 型           |  默认值   |             可选值              |                                       说 明                                       |
| :----------: | :-----------------------: | :-------: | :-----------------------------: | :-------------------------------------------------------------------------------: |
|   percent    |          Number           |     0     |              0-100              |                                  百分比（必填）                                   |
| line-height  |          Number           |     6     |                                 |                                    进度条高度                                     |
|     type     |          String           |  `line`   |         `line` / `lump`         |                                    进度条类型                                     |
|    status    |          String           |           | `success` / `warning` / `error` |                                    进度条状态                                     |
|    color     | String / Array / Function |           |                                 | 进度条颜色；当使用`Array`时，限制个数为 6；当使用 `Function` 时，参数为 `percent` |
|  color-flow  |          Boolean          |  `false`  |                                 |                                 是否开启颜色流动                                  |
| flow-second  |          Number           |     5     |               1-6               |                        流动所需时间，即时间越小，速度越快                         |
|   bg-color   |          String           | `#ebeef5` |            颜色代码             |                                  进度条背景颜色                                   |
|    border    |          Boolean          |  `true`   |                                 |                                     是否圆弧                                      |
|  show-text   |          Boolean          |  `true`   |                                 |                                是否显示进度条文字                                 |
|    format    |         Function          |           |                                 |                         自定义文字显示，参数为 `percent`                          |
|  cut-width   |          Number           |     1     |                                 |                                    `lump` 宽度                                    |
|  cut-color   |          String           | `#ebeef5` |            颜色代码             |                                    `lump` 颜色                                    |
|    active    |          Boolean          |  `false`  |                                 |                                   是否开启动效                                    |
| active-color |          String           |           |                                 |                                     动效颜色                                      |

## 📒 更新日志
- [vue2](https://github.com/xrkffgg/k-progress/blob/master/CHANGELOG-CN.md)
- [vue3](https://github.com/xrkffgg/k-progress-v3/blob/main/CHANGELOG-CN.md)

## GitHub
- [vue2](https://github.com/xrkffgg/k-progress)
- [vue3](https://github.com/xrkffgg/k-progress-v3)