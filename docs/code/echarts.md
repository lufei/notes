# ECharts

## 异步加载data数据

ECharts中的数据是在初始化后setOption中直接填入的，但是很多时候可能数据需要异步加载后再填入。

在图表初始化后不管任何时候只要通过 jQuery 等工具异步获取数据后通过 setOption 填入数据和配置项就行。

```javascript
function functionName(_id) {
    var myChart = echarts.init(document.getElementById('_id'));
    
    $.ajax({
        type: 'GET',
        dataType: 'json',
        url: '/url/' + _id,
        success: function (result) {
            if (result.code == 200) {
                myChart.setOption({
                    series: [{
                        data: result.data
                    }],
                });
            }
        }
    });
    
    option = {
        tooltip: {
            trigger: 'item',
            formatter: '{b} : {c} ({d}%)'
        },
        legend: {
            orient: 'vertical',
            left: 'left',
        },
        series: [
            {
                type: 'pie',
                radius: '55%',
                center: ['50%', '60%'],
                data: [],
                emphasis: {
                    itemStyle: {
                        shadowBlur: 10,
                        shadowOffsetX: 0,
                        shadowColor: 'rgba(0, 0, 0, 0.5)'
                    }
                }
            }
        ]
    };
    myChart.setOption(option);
}
```

## 修改x轴和y轴的颜色

```javascript
xAxis: {
    type: 'value',
    boundaryGap: [0, 0.01],
    //设置轴线的属性
    axisLine:{
        lineStyle:{
            color:'red',
        }
    }
},
yAxis: {
    type: 'category',
    data: ['巴西', '印尼', '美国', '印度', '中国', '世界人口(万)'],
    //设置轴线的属性
    axisLine:{
        lineStyle:{
            color:'red',
        }
    }
},
```

## 修改legend颜色

```javascript
legend: {
    data: ['2011年', '2012年'],
    textStyle: {
        color:'red'
    },
},
```

## 修改legend样式(正方形、矩形、圆形等)

```javascript
legend: {
    data: [
        {
            name: '2011年',
            icon: 'triangle',
        },
        {
            name: '2012年',
            icon: 'triangle'
        }
    ]
},
```

|   icon    |    展示    |
| :-------: | :--------: |
|  circle   |    圆形    |
|   rect    |    矩形    |
| roundRect |  圆角矩形  |
| triangle  |   三角形   |
|  diamond  |    菱形    |
|    pin    |    水滴    |
|   arrow   |    箭头    |
|   none    | 不显示图标 |
