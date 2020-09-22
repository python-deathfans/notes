## Pie()

+ 参数
  + `radius`:Optional[Sequence] = None
    + 饼图的半径，数组的第一项是内半径，第二项是外半径
    + 默认设置成百分比
  + `center`: Optional[Sequence] = None
    + 饼图的`中心坐标`，第一项是`横坐标`，第二项是`纵坐标`
    + 默认设置成百分比，设置成百分比时第一项是相对于容器宽度，第二项是相对于容器高度
  + `rosetype`: Optional[str] = None
    + 是否展示成南丁格尔图，通过半径区分数据大小，有'radius'和'area'两种模式
    + `radius`：扇区圆心角展现数据的百分比，半径展现数据的大小
    + `area`：所有扇区圆心角相同，仅通过半径展现数据大小

### 环形饼状图

```python
x_data = Faker.choose()
y_da = Faker.values().sort()

pie = (
    Pie(init_opts=opts.InitOpts(theme='dark'))
    .add("", [list(z) for z in zip(x_data, y_data)], radius=['40%', '60%'])
    .set_global_opts(
        legend_opts=opts.LegendOpts(orient='vertical', pos_top='15%', pos_left='2%'),
        toolbox_opts=opts.ToolboxOpts()
    )
    .set_series_opts(label_opts=opts.LabelOpts(formatter="{b}: {d}%"))
)

pie.render_notebook()
```

![](https://pic.downk.cc/item/5f58308b160a154a67d1e517.png)

### 玫瑰图

```python
x_data = Faker.choose()
y_da = Faker.values().sort()

pie = (
    Pie(init_opts=opts.InitOpts(theme='dark'))
    .add("", [list(z) for z in zip(x_data, y_data)], radius=['35%', '75%'], rosetype='radius')
    .set_global_opts(
        legend_opts=opts.LegendOpts(orient='vertical', pos_top='15%', pos_left='2%'),
        toolbox_opts=opts.ToolboxOpts()
    )
    .set_series_opts(label_opts=opts.LabelOpts(formatter="{b}: {d}%"))
)

pie.render_notebook()
```

![](https://pic.downk.cc/item/5f583193160a154a67d2143b.png)

### 多饼图

```python
pie=(
    Pie(init_opts=opts.InitOpts(theme='dark'))
        .add(
            "",
            [list(z) for z in zip(["剧情", "其他"], [25, 75])],
            center=["20%", "30%"],
            radius=[40, 60],
        )
        .add(
            "",
            [list(z) for z in zip(["奇幻", "其他"], [24, 76])],
            center=["55%", "30%"],
            radius=[40, 60],
        )
        .add(
            "",
            [list(z) for z in zip(["爱情", "其他"], [14, 86])],
            center=["20%", "70%"],
            radius=[40, 60],
        )
        .add(
            "",
            [list(z) for z in zip(["惊悚", "其他"], [11, 89])],
            center=["55%", "70%"],
            radius=[40, 60],
        )
        .set_global_opts(
            title_opts=opts.TitleOpts(title="Pie-多饼图基本示例"),
            legend_opts=opts.LegendOpts(
                type_="scroll", pos_top="center", pos_left="80%", orient="vertical"
            ),
            toolbox_opts=opts.ToolboxOpts()
        )
        .set_series_opts(label_opts=opts.LabelOpts(formatter="{b}: {c}"))
    )

pie.render_notebook()
```

![](https://pic.downk.cc/item/5f583418160a154a67d2860d.png)



## 下载图片

```python
bar = Bar()

bar.add_xaxis(cate)
bar.add_yaxis("online", data1, stack=True)
bar.add_yaxis("offline", data2, stack=True)

toolbox_opts=opts.global_options.ToolBoxFeatureOpts(
    save_as_image = {"show": True, "title": "save as image", "type": "png"})

bar.set_global_opts(title_opts=opts.TitleOpts(title='销量', subtitle='品牌'), 
                    legend_opts=opts.LegendOpts(is_show=True, legend_icon='circle', orient='horizontal'),
                    tooltip_opts=opts.TooltipOpts(is_show=True, background_color='green', formatter="{b}: {c}"),
                    toolbox_opts=opts.ToolboxOpts(feature=toolbox_opts)
                   )

bar.render_notebook()
```

## TimeLine()

```python
begin = datetime.date(2020, 4, 1)
end = datetime.date(2020, 4, 20)

x_data = Faker.choose()

def get_random_data(n):
    return list(random.randint(100, 200) for _ in range(n))

tl = Timeline()
tl.add_schema()

for i in range((end-begin).days+1):
    day = begin+datetime.timedelta(days=i)
    
    bar = (
        Bar()
        .add_xaxis(x_data)
        .add_yaxis("online", get_random_data(len(x_data)))
    )
    
    tl.add(bar, day)
   
tl.render_notebook()
```



## Faker类

```python
from pyecharts.faker import Faker
```

+ Faker.choose()
  + ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
+ Faker.values()
  + [22, 148, 43, 81, 143, 60, 93]
+ Faker.country()
  + ['China', 'Canada', 'Brazil', 'Russia', 'United States', 'Africa', 'Germany']

## 标签显示不完整

```python
bar = (Bar()
       .add_xaxis(x_data)
       .add_yaxis('', y_data)
       .set_global_opts(xaxis_opts=opts.AxisOpts(
    axislabel_opts=opts.LabelOpts(rotate=-30)
))
       )

bar.render()
```

## 增加一个y轴

```python
bar = Bar()

bar.add_xaxis(x_data)
# 指定index, 默认是0
bar.add_yaxis("", Faker.values(), yaxis_index=0)

# 增加一个y轴
bar.extend_axis(
    yaxis=opts.AxisOpts(
        type_='value',
        position='right'
    )
)

line = Line()

line.add_xaxis(x_data)
line.add_yaxis("", Faker.values(), yaxis_index=1, z_level=1)

bar.overlap(line)
bar.render()
```

## 坐标轴配置项

+ `参数`
  + 坐标轴类型`type_`
    + '`value`': 数值轴，适用于`连续数据`。
    + '`category`': 类目轴，适用于`离散的类目数据`，为该类型时必须通过 data 设置类目数据
    + '`time`': 时间轴，适用于`连续的时序数据`，与数值轴相比时间轴带有时间的格式化，在刻度计算上也有所不同，例如会根据跨度的范围来决定使用月，星期，日还是小时范围的刻度。
  + 坐标轴名称
    + `name`
  + 坐标轴名称文本样式：
    name_textstyleopts=opts.TextStyleOpts(color='red')
  + `刻度最大最小值`
    + min,max_
  + 坐标轴标签（配置代码需要放在xaxis_opts 或 yaxis_opts内）
    更多的标签配置请参考「系列配置项——LabelOpts-标签配置项」
    注意，axislabel_opts配置要放在xaxis_opts里面配置
    axislabel_opts=opts.LabelOpts(
    color='red',
    font_size=10))
  + 坐标轴轴线（配置代码需要放在xaxis_opts 或 yaxis_opts内)
    这个单独拿出来讲
  + 坐标轴刻度（配置代码需要放在xaxis_opts 或 yaxis_opts内）
    这个单独拿出来讲

```python
from pyecharts.charts import Bar
from pyecharts import options as opts

# 示例数据
x_data = ['Apple', 'Huawei', 'Xiaomi', 'Oppo', 'Vivo', 'Meizu']
y_data_1 = [123, 153, 89, 107, 98, 23]
y_data_2 = [231, 321, 135, 341, 245, 167]

bar = Bar()
bar.add_xaxis(x_data)
bar.add_yaxis("online", y_data_1)
bar.add_yaxis("offline", y_data_2)
bar.set_global_opts(
    xaxis_opts=opts.AxisOpts(
        type_="category",
        name="品牌",
        name_textstyle_opts=opts.TextStyleOpts(
            color='red'
        )
    ),
    yaxis_opts=opts.AxisOpts(
        name="销售额/万元",
        name_textstyle_opts=opts.TextStyleOpts(
            color='red'
        ),
        min_=20,
        max_=500
    )
)

bar.render()
```

## 文字样式配置项：TextStyleOpts

字体配置选项，`主要参数`：

+ title_textstyle_opts=opts.TextStyleOpts(color='red')
+ title_textstyle_opts=opts.TextStyleOpts(font_style="italic")) # 可选：'normal'，'italic'，'oblique'
+ title_textstyle_opts=opts.TextStyleOpts(font_weight="lighter"）
+ title_textstyle_opts=opts.TextStyleOpts(font_size=30)
+ title_textstyle_opts=opts.TextStyleOpts(font_family="serif")

## Faker模块

+ Faker.choose
  + ![](https://pic.downk.cc/item/5f557839160a154a673b7ff5.png)

+ Faker.values()
  + ![](https://pic.downk.cc/item/5f557874160a154a673b877f.png)