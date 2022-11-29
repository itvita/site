---
title: xTable
categories:
  - xtools-antd
  - vue
tags:
  - vue
mp3: /music/C400000v9eTA0esGpv.m4a
cover: /img/104203-1667702523e4a0.jpg
date: 2022-10-09 19:44:53
---

1. [示例](#示例)
2. [代码](#代码)
3. [属性](#属性)
   1. [columns](#columns)
   2. [action](#action)
   3. [formatter 示例](#formatter-示例)
      1. [格式化为文本](#格式化为文本)
      2. [格式化为徽章](#格式化为徽章)
      3. [格式化为图片](#格式化为图片)
4. [事件](#事件)
5. [方法](#方法)
## 示例
![](https://cdn.jsdelivr.net/gh/itvita/resources@master/images/202201211649098.png)
## 代码
```html
 <x-table
      ref="myTable"
      title="菜单列表"
      :columns="columns"
      :action="action"
      :expandedRowDetail="2"
       :scrollX="1280"
      :scrollY="300"
      data-url="https://getman.cn/mock/my/table3">
      <a-space slot="tools">
        <a-button icon="plus" type="primary">
          添加
        </a-button>
        <a-button icon="delete" type="danger">
          批量删除
        </a-button>
      </a-space>
    </x-table>
```
```javascript
const columns = [
  {
    title: '名称',
    key: 'accountName',
    align: 'left',
    sorter: true,
    width: 180,
    formatter: { // 文本格式化显示
      type: 'text',
      format: row => {
        return {
          value: row.accountName, // 显示文本（必填）
          color: '#1890ff', // 显示颜色link,error,wain, rgb , hex
          event: () => { // 点击触发事件
            console.log(row.accountName)
          }
        }
      }
    }
  },
  {
    title: '状态',
    key: 'state',
    align: 'center',
    sorter: true,
    width: 180,
    formatter: { // 文本格式化显示
      type: 'badge',
      format: row => {
        if (row.state === 1) {
          return {
            value: '启用', // 显示文本（必填）
            color: 'blue', // 徽章颜色'blue','green','gray','orange','yellow','red' 等支持16进制
            event: () => { // 点击触发事件
              console.log(row.state)
            }
          }
        } else {
          return {
            value: '禁用', // 显示文本（必填）
            color: 'red' // 徽章颜色'blue','green','gray','orange','yellow','red' 等支持16进制
          }
        }
      }
    }
  },
  {
    title: '图片格式化测试',
    key: 'images',
    align: 'left',
    sorter: true,
    width: 180,
    formatter: {
      type: 'image', // 格式化方式
      width: '28px', // 图片显示宽度，不设置默认50px
      height: '28px', // 图片显示高度，不设置默认50px
      format: row => {
        return [
          {
            name: '图片提示名称', // 名称
            url: 'https://norisk-prod-1305901002.cos.ap-chengdu.myqcloud.com/20220119/014026340563464bb7ee74d653325825.png' // 图片路径
          },
          {
            url: 'https://norisk-prod-1305901002.cos.ap-chengdu.myqcloud.com/20220119/014026340563464bb7ee74d653325825.png' // 图片路径
          }
        ]
      }
    }
  },
  {
    title: '区域名称',
    key: 'areaName',
    align: 'center', // 对齐方式
    sorter: true, // 是否可以排序
    width: 150, // 宽度，数字或百分比
    ellipsis: 1,
    hide: false// 从列表中隐藏该列
  },
  {
    title: '时间',
    key: 'createdTime',
    align: 'center',
    width: 150 // 宽度，数字或百分比
  },
  {
    title: '地址',
    key: 'cmpAddress',
    align: 'left',
    ellipsis: 2,
    width: 150 // 宽度，数字或百分比
  }
]
const action = [
  {
    title: '修改',
    icon:'edit',//显示图标，目前仅支持官方图标库，moren edit
    color: 'link', // 显示颜色link,error,wain, rgb , hex
    permission:'edit',
    event: row => {
      console.log(row)
    }
  },
  {
    title: '删除',
    color: 'error', // 显示颜色link,error,wain, rgb , hex
    event: row => {
      console.log(row)
    },
    hidden: row => {
      console.log(row)
      if (row.id % 2 === 0) {
        return true
      }
        return false
    }
  },
  {
    title: '其他',
    color: 'wain', // 显示颜色link,error,wain, rgb , hex
    event: row => {
      console.log(row)
    }
  }
]
export default {
  data () {
    return {
      columns,
      action
    }
  },
  mounted () {
    this.$refs.myTable.search({ headers: {}, params: {} })
  },
  methods: {
    search (params) {
      console.log(params)
    }
  }
}
```
## 属性

| 属性              | 说明                               | 类型             | 默认值   |
| ----------------- | ---------------------------------- | ---------------- | -------- |
| title             | 列表标题                           | String           | 查询列表 |
| columns           | 列配置                             | Array            | []       |
| action            | 操作配置                           | Array            | []       |
| expandedRowDetail | 默认详情操作按钮（0不显示，1显示） | Number           | 0        |
| rowKey            | 行键 同antd-table                  | String，function | id       |
| selection         | 开启选择框 [checkbox,radio]        | String           |          |
| showIndex         | 显示序号                           | Boolean          | false    |
| dataUrl           | 数据请求地址                       | String           |          |
| actionWidth       | 操作列宽                           | Number           | 120      |
| scrollX           | 滚动区域宽                         | Number           | 960      |
| scrollY           | 滚动区域高                         | Number           | 800      |
| data-source       | 默认数据                           | array            | []       |


### columns
| 属性      | 说明         | 类型           | 可选                 | 默认值 |
| --------- | ------------ | -------------- | -------------------- | ------ |
| title     | 列名称       | String         |                      |
| key       | 键           | String         |                      |
| align     | 对齐方式     | String         | left，center,right   | left   |
| sorter    | 是否开启排序 | Boolean        | true，false          | false  |
| width     | 列宽         | Number，String | 像素或百分比         | 自适应 |
| ellipsis  | 超出省略     | Number         | 设置为0或false则全显 | 1      |
| hide      | 隐藏列       | Boolean        |                      | false  |
| formatter | 内容格式化   | Object         |                      |


### action
| 属性       | 说明         | 类型               | 可选                               | 默认值 |
| ---------- | ------------ | ------------------ | ---------------------------------- | ------ |
| title      | 操作名称     | String             |                                    |        |
| icon       | 显示图标     | String             | antd-icon                          |        |
| color      | 文字颜色     | String             | 显示颜色link,error,wain, rgb , hex |        |
| permission | 权限标识     | String             |                                    |        |
| event      | 点击事件     | row=>{}            |                                    |        |
| hidden     | 动态隐藏条件 | row=>{return true} |                                    | true   |


### formatter 示例
#### 格式化为文本
```javascript
formatter: { // 文本格式化显示
      type: 'text',
      format: row => {
        return {
          value: row.accountName, // 显示文本（必填）
          color: '#1890ff', // 显示颜色link,error,wain, rgb , hex
          event: () => { // 点击触发事件
            console.log(row.accountName)
          }
        }
      }
    }
```
#### 格式化为徽章
```javascript
    formatter: { // 文本格式化显示
      type: 'badge',
      format: row => {
        if (row.state === 1) {
          return {
            value: '启用', // 显示文本（必填）
            color: 'blue', // 徽章颜色'blue','green','gray','orange','yellow','red' 等支持16进制
            event: () => { // 点击触发事件
              console.log(row.state)
            }
          }
        } else {
          return {
            value: '禁用', // 显示文本（必填）
            color: 'red' // 徽章颜色'blue','green','gray','orange','yellow','red' 等支持16进制
          }
        }
      }
    }
```
#### 格式化为图片
```javascript
formatter: {
      type: 'image', // 格式化方式
      width: '28px', // 图片显示宽度，不设置默认50px
      height: '28px', // 图片显示高度，不设置默认50px
      format: row => {
        return [
          {
            name: '图片提示名称', // 名称
            url: 'https://norisk-prod-1305901002.cos.ap-chengdu.myqcloud.com/20220119/014026340563464bb7ee74d653325825.png' // 图片路径
          },
          {
            url: 'https://norisk-prod-1305901002.cos.ap-chengdu.myqcloud.com/20220119/014026340563464bb7ee74d653325825.png' // 图片路径
          }
        ]
      }
    }
```

## 事件

| 事件名称     | 说明   | 回调参数                                |
| ------------ | ------ | --------------------------------------- |
| rowSelection | 行选择 | function(selectedRowKeys，selectedRows) |
> selectedRowKeys 选中行 key

> selectedRows 选中行数据

## 方法

| 方法名称 | 说明         | 举例                                                   |
| -------- | ------------ | ------------------------------------------------------ |
| search   | 获取查询条件 | this.$refs.myTable.search({ headers: {}, params: {} }) |

> headers 主要用于增加token

> params 搜索条查询条件，或其他来源查询条件，分页排序条件已内置