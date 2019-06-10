# components

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### 参数说明
### input
|   参数     | 取值            |
|  ----     | ----            |
| type      | text/password   | 
| label     | 说明文字         |
| v-model   | 绑定的输入值     |

###select
|   参数    | 取值            |
|  ----     | ----            |
| options   | 内容数组         | 
| label     | 说明文字         |
| v-model   | 绑定的输入值     |

###switch
|   参数    | 取值            |
|  ----     | ----            |
| oncolor   | 开启时的背景颜色  | 
| offcolor  | 关闭时的背景颜色  |
| label     | 说明文字         |
| v-model   | true开启，false关闭 |

###progress
|   参数    | 取值            |
|  ----     | ----            |
| percent   | 进度条百分比     | 
| color     | 进度条背景颜色   |

###badge
|   参数    | 取值            |
|  ----     | ----            |
| value     | 标记数目         | 
| color     | 标记块的颜色     |

###button
|   参数    | 取值            |
|  ----     | ----            |
| type      | normal/success/info/warning/danger         | 
| size      | big/middle/small     |

###datepicker
|   参数    | 取值            |
|  ----     | ----            |
| v-model   | 选择的日期 |

###slider
|   参数    | 取值            |
|  ----     | ----            |
| color     | 滑动条颜色 | 
| v-model   | 滑动条位置。取值0-100 |

###pagination
|   参数    | 取值            |
|  ----     | ----            |
| total     | 总条目数 | 
| pagenumber| 每页条目数|
| v-model   | 当前页数 |
| sizeChange| 绑定的事件。在当前页改变的时候触发|

###radio
|   参数    | 取值            |
|  ----     | ----            |
| data     | 内容数组 | 
| type     | pointer/button|
| v-model   | 当前选择的是第几个 |

###radio
|   参数    | 取值            |
|  ----     | ----            |
| data     | 内容数组 | 
| type     | pointer/button|
| v-model   | 当前选择的是哪几个 |