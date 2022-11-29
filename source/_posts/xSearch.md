---
title: xsearch
categories:
  - xtools-antd
  - vue
tags:
  - vue
mp3: /music/C400002D61HP2ybLAC.m4a
cover: /img/234549-1669045549622d.jpg
date: 2022-10-09 19:44:53
---

## 示例
![](https://cdn.jsdelivr.net/gh/itvita/resources@master/images/202201211649098.png)

## 代码
```html
 <x-search ref="mySearch" :search-items="searchItems" :label-width="100" @search="search"></x-search>
```

```javascript
const searchItems = [
  {
    type: 'text',
    key: 'name',
    label: '文本',
    value: '张三',
    placeholder: '提示文字'
  },
  {
    type: 'select',
    key: 'sex',
    label: '下拉',
    value: '',
    placeholder: '请选择',
    options: [
      {
        label: '男',
        value: '1'
      },
      {
        label: '女',
        value: '2'
      }
    ]
  },
  {
    type: 'select',
    key: 'sex1',
    label: '动态下拉',
    value: '',
    placeholder: '请选择',
    options: []
  },
  {
    type: 'rangePicker',
    key: 'rangeDate',
    label: '日期范围',
    value: ['2022-01-21 00:00:00', '2022-01-31 23:59:59']
  },
  {
    type: 'cascader',
    key: 'address',
    label: '级联下拉',
    value: [],
    options: [
      {
        id: '1',
        parentId: '0',
        label: '河南',
        value: '001'
      },
      {
        id: '2',
        parentId: '1',
        label: '郑州',
        value: '001001'
      },
      {
        id: '3',
        parentId: '2',
        label: '高新区',
        value: '001001001'
      }
    ]
  },
  {
    type: 'cascader',
    key: 'address1',
    label: '动态级联下拉',
    value: [],
    options: []
  }
]
export default {
  data () {
    return {
      searchItems
    }
  },
  mounted () {
    // 模拟延迟加载数据
    setTimeout(() => {
      this.searchItems[2].options = [{
        label: '男',
        value: '1'
      },
        {
          label: '女',
          value: '2'
        }]

      this.searchItems[5].options = [
        {
          id: '1',
          parentId: '0',
          label: '河南',
          value: '001'
        },
        {
          id: '2',
          parentId: '1',
          label: '郑州',
          value: '001001'
        },
        {
          id: '3',
          parentId: '2',
          label: '高新区',
          value: '001001001'
        }
      ]
    }, 3000)
  },
  methods: {
    search (params) {
      console.log(params)
    }
  }
}
```
## 属性

| 属性     | 说明                       | 类型   | 默认值 |
| -------- | -------------------------- | ------ | ------ |
| label-width      | label宽度 | Number | 100   |
| search-items | 组件配置                   | Array  |   []     |

### search-items
| 属性     | 说明                       | 类型   | 可选项 |默认值
| -------- | -------------------------- | ------ | ------ |---|
| type      | 类型 | String |  text,select,rangePicker,cascader  |
| key | 键                   | String  |        |
|label|显示名称|String
|value|值|String,Array|text，select时为String，rangePicker,cascader为Array|
|placeholder|提示文字|String||非必填
|options|select，cascader选项|Array|简单数组|

## 事件

| 事件名称     | 说明               | 回调参数         |
| ------------ | ------------------ | ---------------- |
| search | 搜索 | function(searchFrom) |

## 方法

| 方法名称 | 说明       | 举例                                               |
| ---- | ---------- | -------------------------------------------------- |
| getSearchFrom | 获取查询条件 | this.$refs.mySearch.getSearchFrom() |