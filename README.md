# wx-plugins

**wx-plugins**是一套可添加到小程序内直接使用的功能组件，无需重复开发，为用户提供更丰富的服务。

![yuanful-wx-plugins](https://img.shields.io/badge/license-MIT-blue.svg)


## 插件安装
在`app.json`中配置插件的引入
```json
{
  "pages": [
    "pages/index/index"
  ],
  "plugins": {
    "YuanFul": {
      "version": "1.0.0",
      "provider": "wx2ca7a9c0f8d4e2b9"
    }
  }
}
```

## 插件目录
* [城市选择列表 `city-index-list`](#city-index-list)
* [搜索组件 `searchbar`](#searchbar)



## 插件说明
#### 插件主题颜色值
<p><i style="width:10px;height:10px;display:inline-block;background:#03a9f4"></i> blue <code>#03a9f4</code></p>
<p><i style="width:10px;height:10px;display:inline-block;background:#f19149"></i> orange <code>#f19149</code></p>
<p><i style="width:10px;height:10px;display:inline-block;background:#f44336"></i> red <code>#f44336</code></p>
<p><i style="width:10px;height:10px;display:inline-block;background:#009688"></i> green <code>#009688</code></p>

<details>
<summary id="city-index-list">
  城市选择列表 `city-index-list`
</summary>

  ### 预览
  <div>
    <img width="40%" src="preview/city-index-list.png" />
  </div>

  ### 属性
  名称 | 类型 | 默认 | 描述
  --- | --- | --- | ---
  theme   | String  | `blue`     | 插件主题<br/>支持：`orange`、`red`、`blue`、`green`
  styles  | Object  | `{}`        | 插件自定义样式<br/>支持：`letterBarBackground` 字母索引背景色、`letterColor` 字母默认颜色、`letterActiveColor` 字母选中的颜色、`closerBackground` 关闭按钮背景
  visible | Boolean | `false`     | 是否显示

  ### 事件
  名称 | 参数 | 描述
  --- | --- | ---
  select  | `event` | 选择城市的回调，`event.detail` 为选择的城市数据，包括：`name` 城市名、`code` 城市编码

  ### 使用
  page.wxml
  ```html
  <city-index-list
      theme="orange"
      visible="{{cityVisible}}"
      styles="{{cityStyles}}"
      bind:select="onSelectCity"
  />

  <button bind:tap="onClickBtn">显示</button>
  ```

  page.js
  ```javascript
  Page({
      data: {
          cityVisible: false,
          cityStyles: {
              letterColor: '#fff'
          }
      },
      onClickBtn(){
          this.setData({
              cityVisible: true
          });
      },
      onSelectCity(e){
          let detail = e.detail;

          console.log(detail);
      }
  });
  ```

  page.json
  ```json
  {
    "usingComponents": {
      "city-index-list": "plugin://YuanFul/city-index-list"
    }
  }
  ```

</details>


<details>
<summary id="searchbar">
  搜索组件 `searchbar`
</summary>

  ### 预览
  <div>
    <img width="40%" src="preview/searchbar.png" />
  </div>

  ### 属性
  名称 | 类型 | 默认 | 描述
  --- | --- | --- | ---
  theme   | String  | `blue`     | 插件主题<br/>支持：`orange`、`red`、`blue`、`green`
  visible | Boolean | `false`     | 是否显示
  placeholder | String | `请输入关键字`     | 输入框默认占位文字
  searchValue | String | ``     | 输入框默认值，默认为空
  clearConfirm | Boolean | `true`     | 点击清空是否弹出二次确认框
  confirmConfig | Object | `{ content: '确定要清空吗？' }`     | 清空时二次确认弹窗配置，与`wx.showModal`参数一致

  ### 事件
  名称 | 参数 | 描述
  --- | --- | ---
  search  | `event` | 搜索的回调，`event.detail` 为选择的城市数据，包括：`text` 搜索的文字
  cancel  | `event` | 取消的回调

  ### 使用
  page.wxml
  ```html
  <searchbar
    visible="{{searchbarVisible}}"
    bind:search="onSearch"
  />

  <button bind:tap="onClickBtn">显示</button>
  ```

  page.js
  ```javascript
    Page({
      data: {

      },
      onClickBtn() {
          this.setData({
              searchbarVisible: true
          });
      },
      onSearch(e) {
          let detail = e.detail;

          console.log(detail);
      }
  })
  ```

  page.json
  ```json
  {
    "usingComponents": {
      "searchbar": "plugin://YuanFul/searchbar"
    }
  }
  ```

</details>