### Dropdown 下拉菜单

#### 概述

展示一组折叠的下拉菜单。

### API

#### Dropdown props
属性|说明|类型|默认值
---|---|---|---
dData|显示下拉菜单所需数据|Array|空
trigger|触发方式，可选值为 hover（悬停）click（点击）|String|hover
hasFolderIcon|是否显示文件夹图标|Boolean|false

##### data structure
属性|说明|类型|默认值
---|---|---|---
des|列表中将要显示的名称|String|null

注：传入`data`前须对其每个元素增加一个名称为`des`的属性，其值为列表中将要显示的名称

#### Dropdown events

名称|说明|返回值
---|---|---
select|点击菜单项时触发|菜单项的所有数据

#### 其他

默认宽度150px，如需自定义，使用内联样式