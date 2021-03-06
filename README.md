### Dropdown 下拉菜单

#### 概述

展示一组折叠的下拉菜单。

### API

#### Dropdown props
属性|说明|类型|默认值
---|---|---|---
dData|显示下拉菜单所需数据|Array|空
trigger|触发方式，可选值为 hover（悬停）click（点击）|String|'hover'
hasFolderIcon|是否显示文件夹图标|Boolean|false
height|下拉列表高度|Number|250

##### dData 说明
属性|说明|类型|默认值
---|---|---|---
des|列表中将要显示的名称|String|-
dis|禁用该项|Boolean|false

注：传入`dData`前须对其每个元素增加一个名称为`des`的属性，其值为列表中将要显示的名称，例：
```html
dData: [
          {
            des: '测试1'
          },
          {
            des: '测试2',
            dis: true // 禁用
          }
        ]
```

#### Dropdown events

名称|说明|返回值
---|---|---
select|点击菜单项时触发|菜单项的所有数据

#### 其他

默认宽度150px，如需自定义，使用内联样式