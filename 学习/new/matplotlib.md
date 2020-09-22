## 折线图

**plt.plot(x,y,color,linestyle,linewidth,marker,markersize,markeredgecolor,markeredgewidth,markerfacecolor,label)**

- x：横坐标数据
- y：纵坐标数据
- linestyle：线条样式（'-' , '.' , '-.' , '--' 等)
- linewidth：线条宽度
- marker：节点样式('o'圈标记 , '.'点标记 , 'v'下三角 , '^'上三角 , 's'正方形等)
- markersize：节点大小
- markeredgecolor：标记外边颜色
- markeredgewidth：标记外边线宽
- markerfacecolor：标记填充颜色
- label：图例名称

## 注释

matplotlib.pyplot.text(x, y, s, fontdict=None, withdash=False, **kwargs)

+ x, y: 需要显示内容的坐标
+ s: 需要显示的内容
+ fontdict: 一个定义s格式的dict
+ `ha`: 设置水平对齐方式
  + left
  + right
  + center
+ `va`: 设置垂直对齐方式
  + center
  + top
  + bottom
  + baseline
+ `rotation`
  + vertical
  + horizontal
  + 数字
+ `alpha`
  + 透明度
  + 0-1之间

## 柱状图

**plt.bar(x,height,width=0.8,bottom=None,align='center',color,edgecolor)**

- x：在什么位置显示柱形图；
- height：每根柱子的高度；
- width：每根柱子的宽度，可以一样，也可以各不相同；
- `bottom`：每根柱子底部位置，可以一样，也可以各不相同；
  - 如果设置堆叠条形图，可以使用这个
- align：柱子的位置与x值的关系，有center、edge可选；
- color：柱子颜色；
- edgecolor：柱子边框颜色。

## 饼图

**plt.pie(x,explode,labels,colors,autopct,pctdistance,shadow,labeldistance, startangle,radius,counterclock,wedgeprops,textprops,center,frame)**

- x：待绘图数据；
- explode：每一块离圆心距离；
- labels：每一块标签；
- colors：每一块颜色；
- autopct：饼图内数值的百分比格式；
- pctdistance：数据标签距中心的距离；
- shadow：是否有阴影；
- labeldistance：每一块索引距中心的距离；
- startangle：饼图的初始角度；
- radius：饼图的半径；
- counterclock：是否逆时针显示；
- wedgeprops：内外边界属性；
- textprops：文本相关属性；
- center：中心位置；
- frame：是否显示背后的图框。

