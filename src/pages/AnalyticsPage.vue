<template>
  <div class="header">
    <h1>Аналитика</h1>
  </div>

  <div id="chartdiv"><div class="chart__title">Аналитика по визитам</div></div>

  <div class="chart__subtitle">
    График визитов
  </div>
</template>

<script>
import * as am5 from '@amcharts/amcharts5';
import * as am5xy from '@amcharts/amcharts5/xy';
import am5themes_Animated from '@amcharts/amcharts5/themes/Animated';


export default {
  name: 'AnalyticsPage',
  mounted() {
    am5.ready(function() {


    // Create root element
    // https://www.amcharts.com/docs/v5/getting-started/#Root_element
    var root = am5.Root.new("chartdiv");

    // Set themes
    // https://www.amcharts.com/docs/v5/concepts/themes/
    root.setThemes([
      am5themes_Animated.new(root)
    ]);


    // Create chart
    // https://www.amcharts.com/docs/v5/charts/xy-chart/
    var chart = root.container.children.push(am5xy.XYChart.new(root, {
      panX: true,
      panY: true,
      wheelX: "panX",
      wheelY: "zoomX",
      pinchZoomX:true
    }));

    // Add cursor
    // https://www.amcharts.com/docs/v5/charts/xy-chart/cursor/
    var cursor = chart.set("cursor", am5xy.XYCursor.new(root, {
      behavior: "none"
    }));
    cursor.lineY.set("visible", false);

    // Create axes
    // https://www.amcharts.com/docs/v5/charts/xy-chart/axes/
    var xAxis = chart.xAxes.push(am5xy.DateAxis.new(root, {
      maxDeviation: 0.5,
      baseInterval: {
        timeUnit: "day",
        count: 1
      },
      renderer: am5xy.AxisRendererX.new(root, {
      pan:"zoom"
    }),
      tooltip: am5.Tooltip.new(root, {})
    }));

    var yAxis = chart.yAxes.push(am5xy.ValueAxis.new(root, {
      maxDeviation:1,
      renderer: am5xy.AxisRendererY.new(root, {
      pan:"zoom"
    })
    }));


    // Add series
    // https://www.amcharts.com/docs/v5/charts/xy-chart/series/
    var series = chart.series.push(am5xy.SmoothedXLineSeries.new(root, {
      xAxis: xAxis,
      yAxis: yAxis,
      valueYField: "visits",
      valueXField: "date",
      tooltip: am5.Tooltip.new(root, {
        labelText: "Кол-во визитов: {valueY}"
      })
    }));

    series.fills.template.setAll({
      visible: true,
      fillOpacity: 0.5,
      fill: '#006DFE',
    });

    series.bullets.push(function() {
      return am5.Bullet.new(root, {
        locationY: 0,
        sprite: am5.Circle.new(root, {
          radius: 5,
          stroke: '#fff',
          strokeWidth: 1,
          fillOpacity: 0.5,
          fill: "#006DFE"
        })
      });
    });


    // Add scrollbar
    // https://www.amcharts.com/docs/v5/charts/xy-chart/scrollbars/
    chart.set("scrollbarX", am5.Scrollbar.new(root, {
      orientation: "horizontal"
    }));

    var data = [
      {"date":"2020-07-01","visits":213},
      {"date":"2020-07-02","visits":249},
      {"date":"2020-07-03","visits":179},
      {"date":"2020-07-04","visits":170},
      {"date":"2020-07-05","visits":184},
      {"date":"2020-07-06","visits":202},
      {"date":"2020-07-07","visits":198},
      {"date":"2020-07-08","visits":168},
      {"date":"2020-07-09","visits":176},
      {"date":"2020-07-10","visits":171},
      {"date":"2020-07-11","visits":190},
      {"date":"2020-07-12","visits":154},
      {"date":"2020-07-13","visits":246},
      {"date":"2020-07-14","visits":250},
      {"date":"2020-07-15","visits":227},
      {"date":"2020-07-16","visits":140},
      {"date":"2020-07-17","visits":170},
      {"date":"2020-07-18","visits":125},
      {"date":"2020-07-19","visits":106},
      {"date":"2020-07-20","visits":207},
      {"date":"2020-07-21","visits":222},
      {"date":"2020-07-22","visits":198},
      {"date":"2020-07-23","visits":204},
      {"date":"2020-07-24","visits":213},
      {"date":"2020-07-25","visits":145},
      {"date":"2020-07-26","visits":166},
      {"date":"2020-07-27","visits":163},
      {"date":"2020-07-28","visits":135},
      {"date":"2020-07-29","visits":45}
    ];

    series.data.processor = am5.DataProcessor.new(root, {
      dateFormat: "yyyy-MM-dd",
      dateFields: ["date"]
    });

    series.data.setAll(data);

    // Make stuff animate on load
    // https://www.amcharts.com/docs/v5/concepts/animations/
    series.appear(1000);
    chart.appear(1000, 100);

    }); // end am5.ready()
  },

  beforeDestroy() {
    if (this.root) {
      this.root.dispose();
    }
  }
}
</script>

<style scoped lang="scss">
#chartdiv {
  width: 100%;
  height: 500px;
}

.chart__title  {
  font-weight: 500;
  font-size: 24px;
  text-align: center;
  margin: 30px 0;
}

.chart__subtitle {
  font-weight: 500;
  font-size: 24px;
  text-align: left;
  margin: 60px 0 0 0;
}
</style>
