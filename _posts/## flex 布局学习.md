##  flex 布局学习

## flex布局是什么：
        flex布局是弹性布局用来为盒状模型提供最大的灵活性，任何一个容器都可以指定为flex布局，行内元素也能使用flex布局
        容器默认两根轴，水平的主轴和垂直的交叉轴，主轴开始的地方叫main start ，结束的地方叫main end，交叉轴开始的地方叫cross start，结束的地方叫cross end

## flex容器属性
        六个属性：
                1.flex-direction (flex方向，确定主轴的方向)
                                                        row（默认值）：主轴为水平方向，起点在左端。
                                                        row-reverse：主轴为水平方向，起点在右端。
                                                        column：主轴为垂直方向，起点在上沿。
                                                        column-reverse：主轴为垂直方向，起点在下沿。
                
                2.flex-warp (flex弯曲，变形，定义如果一条轴线放不下的话，如何换行)
                                                        nowarp(默认)：,不换行
                                                        warp：第一行在上方，也就是向下排列
                                                        warp-reverse：第一行在下方，向上排列
                3.flex-flow (flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap)
                4.justify-content (项目在主轴上的对齐方式)
                                                        flex-start (默认值):左对齐
                                                        flex-end:右对齐
                                                        center:居中
                                                        space-between:两端对齐，项目之间间隔相等
                                                        space-around:每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍
                5.align-items (对齐项目，定义项目在交叉轴上如何对齐)
                                                        flex-start:交叉轴的起点对齐
                                                        flex-end:交叉轴的终点对齐
                                                        center:交叉轴的中点对齐
                                                        baseline:项目的第一行文字的基线对齐
                                                        stretch(伸展，默认):如果项目未设置高度或者设为aoto，将占满整个容器的高度
                6.align-content (定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用)
## flex项目属性
        六个属性：
                1.order (顺序，定义项目的排列顺序，给他一个int值，数值越小越靠前。)
                2.flex-grow (定义项目的放大比例，默认为0，)
                3.flex-shrink (flex收缩，定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小，负值无效)
                4.flex-basis (定义了在分配多余空间之前，项目占据的主轴空间[main size],浏览器根据这个属性，计算主轴是否有多余空间，默认值为auto，就是项目本来大小)
                5.flex (flex属性是flex-grow，flex-shrink，和flex-basis的简写，默认值为0 1 auto)
                6.align-self (属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性，默认值为auto，表示继承元素的align-items，如果没有父元素，则等同于stretch)
                