##### layout

<description>**optional** _horizontal | vertical_ </description>

图例布局方式。提供横向布局和纵向布局。

##### title

<description>**optional** _G2LegendTitleCfg_ </description>

图例标题配置，默认不展示。_G2LegendTitleCfg_ 配置如下：

| 参数名  | 类型     | 描述                                                         |
| ------- | -------- | ------------------------------------------------------------ |
| text   | _string_ | 文本显示内容                                                 |
| spacing | _number_ | 标题同图例项的间距                                           |
| style   | _object_ | 文本样式配置项，参考  [绘图属性](/zh/docs/api/graphic-style) |

##### position

<description>**optional** _string_ </description>

图例位置，可选项：'top', 'top-left', 'top-right', 'left', 'left-top', 'left-bottom', 'right', 'right-top', 'right-bottom', 'bottom', 'bottom-left', 'bottom-right'。

尝试一下：

<playground path="component/legend/demo/legend-position.jsx" rid="legend-position"></playground>

##### offsetX

<description>**optional** _number_ </description>

图例 x 方向的偏移。

##### offsetY

<description>**optional** _number_ </description>

图例 y 方向的偏移。

##### background

<description>**optional** _LegendBackgroundCfg_ </description>

背景框配置项。_LegendBackgroundCfg_ 配置如下：

| 参数名  | 类型                 | 描述                                                       |
| ------- | -------------------- | ---------------------------------------------------------- |
| padding | _number \| number[]_ | 背景的留白                                                 |
| style   | _ShapeAttr_          | 背景样式配置项, 参考[绘图属性](/zh/docs/api/graphic-style) |

##### flipPage

<description>**optional** _boolean_ </description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，当图例项过多时是否进行分页。(⚠️ 暂不支持多行展示分页)

##### maxRow

<description> _number_ **optional** </description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，当图例项过多分页时，可以设置最大行数（仅适用于 `layout: 'horizontal'`），默认为：1。

##### pageNavigator

<description>**optional** _object_ </description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，图例分页导航器的主题样式设置。_LegendPageNavigatorCfg_ 配置如下：

| 参数名       | 类型                       | 默认值 | 描述                    |
| ------------ | -------------------------- | ------ | ----------------------- |
| marker.style | _PageNavigatorMarkerStyle_ | -      | 分页器指示箭头 样式配置 |
| text.style   | _PageNavigatorTextStyle_   | -      | 分页器页面信息 样式配置 |

**_PageNavigatorMarkerStyle_** 配置如下：

| 参数名          | 类型     | 默认值 | 描述                                                             |
| --------------- | -------- | ------ | ---------------------------------------------------------------- |
| inactiveFill    | _string_ | -      | Fill color of arrow marker when unclickable (inactive status).   |
| inactiveOpacity | _number_ | -      | Fill opacity of arrow marker when unclickable (inactive status). |
| fill            | _string_ | -      | Default fill color of arrow marker (active status).              |
| opacity         | _number_ | -      | Default fill opacity of arrow marker (active status).            |
| size            | _number_ | -      | Size of arrow marker.                                            |

**_PageNavigatorTextStyle_** 配置如下：

| 参数名   | 类型     | 默认值 | 描述                               |
| -------- | -------- | ------ | ---------------------------------- |
| fill     | _string_ | -      | Font color of page navigator info. |
| fontSize | _number_ | -      | Font size of page navigator info.  |

示例：

```ts
pageNavigator: {
  marker: {
    style: {
      // 非激活，不可点击态时的填充色设置
      inactiveFill: '#000',
      inactiveOpacity: 0.45,
      // 默认填充色设置
      fill: '#000',
      opacity: 0.8,
      size: 12,
    },
  },
  text: {
    style: {
      fill: '#ccc',
      fontSize: 8,
    },
  },
},
```

<playground path="component/legend/demo/legend-flippage.ts" rid="page-navigator"></playground>

##### itemHeight

<description>**optional** _number_ _default:_ `null`</description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，图例的高度, 默认为 null。

##### itemWidth

<description>**optional** _number_ _default:_ `null`</description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，图例项的宽度, 默认为 null，自动计算。

##### itemName

<description>**optional** _LegendItemNameCfg_ </description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，图例项 name 文本的配置。_LegendItemNameCfg_ 配置如下：

| 参数名    | 类型       | 默认值  | 描述                                                                |
| --------- | ---------- | ------- | ------------------------------------------------------------------- |
| style     | _((item: ListItem, index: number, items: ListItem[]) => ShapeAttrs) \| ShapeAttrs_             |          | -      | 文本样式配置项                   |
| spacing   | number                                                  |          | -      | 图例项 marker 同后面 name 的间距 |
| formatter | `(text: string, item: ListItem, index: number) => any;` |          |        | 格式化函数                       |

其中, `ShapeAttrs` 详细配置见：[文档](/zh/docs/api/shape/shape-attrs)；`ListItem` 配置如下：

```ts
type ListItem = {
  /**
   * 名称 {string}
   */
  name: string;
  /**
   * 值 {any}
   */
  value: any;
  /**
   * 图形标记 {object|string}
   */
  marker?: Marker | string;
}

type Marker = {
  symbol? string;
  style?: ShapeAttrs;
  spacing?: number;
};
```

##### itemValue

<description>**optional** _LegendItemValueCfg_ </description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，图例项 value 附加值的配置项。_LegendItemValueCfg_ 配置如下：

| 参数名     | 类型       | 默认值  | 描述                                                                |
| ---------- | ---------- | ------- | ------------------------------------------------------------------- |
| alignRight | _boolean_  | `false` | 是否右对齐，默认为 false，仅当设置图例项宽度时生效                  |
| formatter  | _function_ | -       | 格式化函数, `(text: string, item: ListItem, index: number) => any;` |
| style     | _((item: ListItem, index: number, items: ListItem[]) => ShapeAttrs) \| ShapeAttrs_             |          | -      | 文本样式配置项                   |

其中, `ShapeAttrs` 详细配置见：[文档](/zh/docs/api/shape/shape-attrs)；`ListItem` 配置如下：

```ts
type ListItem = {
  /**
   * 名称 {string}
   */
  name: string;
  /**
   * 值 {any}
   */
  value: any;
  /**
   * 图形标记 {object|string}
   */
  marker?: Marker | string;
}

type Marker = {
  symbol? string;
  style?: ShapeAttrs;
  spacing?: number;
};
```

<playground path="component/legend/demo/legend-item-value.ts" rid="legend-item-value"></playground>

##### itemSpacing

<description>**optional** _number_ </description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，控制图例项水平方向的间距。

##### itemMarginBottom

<description>**optional** _number_ </description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，控制图例项垂直方向的间距。

##### label

<description>**optional** _ContinueLegendLabelCfg_ </description>

适用于 <tag color="cyan" text="连续图例">连续图例</tag>，文本的配置项。_ContinueLegendLabelCfg_ 配置如下：

| 参数名  | 类型     | 默认值 | 描述                                                                                                                                          |
| ------- | -------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------- |
| align   | _string_ | -      | 文本同滑轨的对齐方式 <br/> - rail ： 同滑轨对齐，在滑轨的两端 <br/> - top, bottom: 图例水平布局时有效 <br/> - left, right: 图例垂直布局时有效 |
| style   | _object_ | -      | 文本样式配置项，详见  [绘图属性](/zh/docs/api/graphic-style)                                                                                  |
| spacing | _number_ | -      | 文本同滑轨的距离                                                                                                                              |
| formatter  | _(value: any) => string_ | 文本的格式化方式 |


##### marker

<description>**optional** _MarkerCfg \| MarkerCfgCallback_ </description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，图例项的 marker 图标的配置。

`markdown:docs/common/marker.zh.md`


```sign
type LegendItem = { name: string; value: string; } & MarkerCfg;

type MarkerCfgCallback = (name: string, index: number, item: LegendItem) => MarkerCfg;
```

##### radio ✨

<description>**optional** _RadioCfg_ </description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，图例项的末尾展示一个 radio 的按钮 🔘，点击可以实现“图例正选”筛选（聚焦）。

```sign
type RadioCfg = { style: ShapeAttr };
```

##### maxItemWidth

<description> _number_ **optional** </description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，图例项最大宽度设置。

##### maxWidthRatio

<description> _number_ **optional**. 取值范围：[0, 1], 默认: 0.25</description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，图例项容器最大宽度比例（以 view 的 bbox 容器大小为参照）设置，如果不需要该配置，可以设置为 `null`。

##### maxHeightRatio

<description> _number_ **optional**. 取值范围：[0, 1], 默认: 0.25</description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，图例项容器最大高度比例（以 view 的 bbox 容器大小为参照）设置，如果不需要该配置，可以设置为 `null`。

##### maxWidth

<description>**optional** _number_ </description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，图例项容器最大宽度设置。当 layout 等于 'horizontal' 时，生效，当图例项横向排布，超过最大宽度时，会结合 `flipPage: true` 进行分页。实际上，图例项容器最大宽度的计算如下：

```sign
const viewBBox = this.view.viewBBox;
const maxWidth = Math.min(maxWidth, maxWidthRatio * viewBBox.width);
```

##### maxHeight

<description>**optional** _number_ </description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，图例项容器最大高度设置。当 layout 等于 'vertical' 时，生效，当图例项纵向排布，超过最大高度时，会结合 `flipPage: true` 进行分页。实际上，图例项容器最大宽度的计算如下：

```sign
const viewBBox = this.view.viewBBox;
const maxHeight = Math.min(maxHeight, maxHeightRatio * viewBBox.height);
```

##### reversed

<description>**optional** _boolean_ </description>

适用于 <tag color="green" text="分类图例">分类图例</tag>，是否将图例项逆序展示。

##### custom

<description>**optional** _boolean_ </description>

是否为自定义图例，当该属性为 true 时，需要声明 items 属性。

##### items

<description>**optional** _LegendItem[]_ </description>
适用于 <tag color="green" text="分类图例">分类图例</tag>，用户自己配置图例项的内容。_LegendItem_ 配置如下：

| 参数名 | 类型        | 是否必选 | 描述                     |
| ------ | ----------- | -------- | ------------------------ |
| id     | _string_    |          | 唯一值，用于动画或者查找 |
| name   | _string_    | required | 名称                     |
| value  | any         | required | 值                       |
| marker | _MarkerCfg_ |          | 图形标记                 |

`markdown:docs/common/marker.zh.md`

##### min

<description>**optional** _number_ </description>

适用于 <tag color="cyan" text="连续图例">连续图例</tag>，选择范围的最小值。

##### max

<description>**optional** _number_ </description>

适用于 <tag color="cyan" text="连续图例">连续图例</tag>，选择范围的最大值。

##### value

<description>**optional** _number[]_ </description>

适用于 <tag color="cyan" text="连续图例">连续图例</tag>，当前选中的范围。

##### selected ✨ 🆕

<description> _object_ **optional** </description>

图例高亮状态，false 表示默认置灰，默认不设置或为 true 表示高亮，会同步进行数据的筛选展示。

示例：

```ts
legend: {
  selected: {
    '分类一': true,
    '分类二': false,
    '分类三': false,
  }
}
```

<playground path='component/legend/demo/legend-focus.ts' rid='legend-selected'></playground>

##### slidable

<description>**optional** _boolean_  _default:_ `true`</description>

适用于 <tag color="cyan" text="连续图例">连续图例</tag>，滑块是否可以滑动。

##### rail

<description>**optional** _ContinueLegendRailCfg_ </description>

适用于 <tag color="cyan" text="连续图例">连续图例</tag>，图例滑轨（背景）的样式配置项。_ContinueLegendRailCfg_ 配置如下：

| 参数名        | 类型     | 描述                                                                             |
| ------------- | -------- | -------------------------------------------------------------------------------- |
| type          | _string_ | rail 的类型，color, size，默认：'color'                                                       |
| size          | _number_ | 滑轨的宽度                                                                       |
| defaultLength | _number_ | 滑轨的默认长度，默认：100。当限制了 maxWidth,maxHeight 时，不会使用这个属性会自动计算长度 |
| style         | _object_ | 滑轨的样式，参考 [绘图属性](/zh/docs/api/graphic-style)                          |

|**rail.type='color'**| **rail.type='size** |
|---|---|
|![color](https://gw.alipayobjects.com/zos/antfincdn/jwMUDJ63aN/72957823-0148-4b24-bbf4-c756959467d3.png)|![size](https://gw.alipayobjects.com/zos/antfincdn/t%26LwpJHUA6/52de13d5-b232-4efb-aacf-6d673778d92a.png)|

##### track

<description>**optional** _ContinueLegendTrackCfg_ </description>
适用于 <tag color="cyan" text="连续图例">连续图例</tag>，选择范围的色块样式配置项。_ContinueLegendTrackCfg_ 配置如下：

| 参数名 | 类型     | 默认值 | 描述                                                        |
| ------ | -------- | ------ | ----------------------------------------------------------- |
| style  | _object_ | -      | 选定范围的样式，参考 [绘图属性](/zh/docs/api/graphic-style) |

##### handler

<description>**optional** _ContinueLegendHandlerCfg_ </description>
适用于 <tag color="cyan" text="连续图例">连续图例</tag>，滑块的配置项。(暂不支持自定义)

_ContinueLegendHandlerCfg_ 配置如下：

| 参数名 | 类型     | 默认值 | 描述                                                        |
| ------ | -------- | ------ | ----------------------------------------------------------- |
| size   | _number_ | -      | 滑块的大小，默认：10                                                  |
| style  | _object_ | -      | 滑块的样式设置，参考 [绘图属性](/zh/docs/api/graphic-style) |
