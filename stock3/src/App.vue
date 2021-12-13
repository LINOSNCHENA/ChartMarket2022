<template>
  <div class="hello" ref="chartdiv"></div>
</template>

<script>
import * as am4core from "@amcharts/amcharts4/core";
import * as am4charts from "@amcharts/amcharts4/charts";
import am4themes_animated from "@amcharts/amcharts4/themes/animated";
am4core.useTheme(am4themes_animated);

export default {
  name: "HelloWorld",
  mounted() {
    let chart = am4core.create(this.$refs.chartdiv, am4charts.XYChart);
    chart.paddingRight = 20; // ONE
    chart.numberFormatter.numberFormat = "'ZMK'#.#'B'";
    chart.dateFormatter.inputDateFormat = "YYYY-MM-DD";

    let title = chart.titles.create();
    title.text = "MARVIN FINANCIAL PORTFOLIO, $ZMK";
    title.fontSize = 25;
    title.tooltipText = "Sales in millions of US$ during selected period";

    // chart.tooltip = new am4core.Tooltip();
    // chart.tooltip.label.maxWidth = 150;
    // chart.tooltip.label.wrap = true;

    let data = [];
    chart.data = data;
    chart.data = [
      {
        date: "2021-09",
        institutional: 5001.9,
        proRata: 2500,
        sales: 1999,
        value: 600,
      },
      {
        date: "2021-10",
        institutional: 3001.9,
        proRata: 1500,
        sales: 2700,
        value: 1300,
      },
      {
        date: "2021-11",
        institutional: 5001.9,
        proRata: 2000,
        sales: 1599,
        value: 1200,
      },
      {
        date: "2021-12",
        institutional: 3001.9,
        proRata: 900,
        sales: 2500,
        value: 1600,
      },
    ];

    console.log(chart.data);

    let dateAxis = chart.xAxes.push(new am4charts.DateAxis()); // TWO
    dateAxis.renderer.grid.template.disabled = true;
    dateAxis.renderer.grid.template.location = 0;
    dateAxis.renderer.labels.template.rotation = 45;
    dateAxis.renderer.minGridDistance = 10;
    dateAxis.groupData = true;
    dateAxis.align = "left";
    dateAxis.baseInterval = {
      timeUnit: "day",
      count: 10,
    };
    dateAxis.title.text = "Source: Offering #47 on LuSE Market Intelligence";

    let valueAxis = chart.yAxes.push(new am4charts.ValueAxis()); // THREE
    valueAxis.tooltip.disabled = false;
    valueAxis.renderer.minWidth = 5;

    var label = dateAxis.renderer.labels.template; // FOUR
    label.wrap = true;
    label.maxWidth = 85;
    label.color = "green";

    let series1 = chart.series.push(new am4charts.LineSeries()); // FIVE
    series1.dataFields.valueY = "value";
    series1.dataFields.dateX = "date";
    series1.strokeWidth = 6;
    // series1.fill = am4core.color("green");
    series1.tooltipText = "1ACEI_units {name}: [bold]{valueY}[/]";
    series1.name = "ACEI";

    var series2 = chart.series.push(new am4charts.ColumnSeries()); // SIX
    series2.dataFields.valueY = "proRata";
    series2.dataFields.dateX = "date";
    series2.fill = am4core.color("orange");
    series2.stacked = true;
    series2.autoDispose = true;
    series2.animationsEnabled = true;
    series2.tensionX = 1.0;
    series2.showOnInit = false;
  //  series2.tooltipText = "2CECZ_units {name}: [bold]{valueY}[/]";
    series2.name = "CECZ";

    var series3 = chart.series.push(new am4charts.ColumnSeries()); // SEVEN
    series3.dataFields.valueY = "sales";
    series3.dataFields.dateX = "date";
    series3.fill = am4core.color("blue");
   // series3.tooltipText = "3CHIL_Units {name}: [bold]{valueY}[/]";
    series3.name = "CHILANGA";

    // Add legend
    chart.legend = new am4charts.Legend(); // EIGHT

    // Add Colors
    chart.colors.list = [
      am4core.color("#845EC2"),
      am4core.color("#D65DB1"),
      am4core.color("#FF6F91"),
      am4core.color("#FF9671"),
      am4core.color("#FFC75F"),
      am4core.color("#F9F871"),
    ];

    chart.cursor = new am4charts.XYCursor(); // NINE
    chart.cursor.lineX.stroke = am4core.color("red");
    chart.cursor.lineX.strokeWidth = 8;
    chart.cursor.lineX.strokeOpacity = 0.4;
    chart.cursor.lineX.strokeDasharray = "";

    chart.cursor.lineY.stroke = am4core.color("blue");
    chart.cursor.lineY.strokeWidth = 8;
    chart.cursor.lineY.strokeOpacity = 0.4;
    chart.cursor.lineY.strokeDasharray = "";

    // chart.cursor.snapToSeries = [series1, series2, series3];

    let scrollbarX = new am4charts.XYChartScrollbar(); // TEN
    scrollbarX.series.push(series2);
    chart.scrollbarX = scrollbarX;

    // Make bullets grow on hover
    let circleBullet = series1.bullets.push(new am4charts.CircleBullet()); // ELEVEN
    circleBullet.circle.strokeWidth = 2;
    circleBullet.circle.radius = 4;
    circleBullet.circle.fill = am4core.color("#fff");

    let circleBullethover = circleBullet.states.create("hover");
    circleBullethover.properties.scale = 1.3;

    valueAxis.renderer.labels.template.fill = series2.stroke;
    valueAxis.renderer.labels.template.fontSize = 12;
    valueAxis.renderer.grid.template.disabled = true;
    // chart.cursor.yAxis = valueAxis;

    let lineSeries = series2; // TWELVE
    let bullet = lineSeries.bullets.push(new am4charts.Bullet());
    let square = bullet.createChild(am4core.Rectangle);
    square.width = 60;
    square.height = 60;
    square.stroke = am4core.color("yellow");
    square.direction = "top";
    square.horizontalCenter = "middle";
    square.verticalCenter = "middle";
    square.strokeWidth = 23;
    square.fill = am4core.color("maroon");

    console.log("==================|SELECT_XY|===================");
    let bullet1 = series1.bullets.push(new am4charts.CircleBullet());
    let bullet1hover = bullet1.states.create("hover");
    bullet1hover.properties.scale = 1.3;

    let bullet2 = series2.bullets.push(new am4charts.CircleBullet());
    let bullet2hover = bullet2.states.create("hover");
    bullet2hover.properties.scale = 1.3;

    let bullet3 = series3.bullets.push(new am4charts.CircleBullet());
    let bullet3hover = bullet3.states.create("hover");
    bullet3hover.properties.scale = 1.3;

    chart.cursor.behavior = "selectXY";
    chart.cursor.events.on("selectended", function (ev) {
      let range = ev.target.xRange;
      let axis = ev.target.chart.xAxes.getIndex(0);
      let from = axis.getPositionLabel(axis.toAxisPosition(range.start));
      let to = axis.getPositionLabel(axis.toAxisPosition(range.end));
        series1.tooltipText =
        "41_units {name}: [bold]{valueY}[/]  42_units {name}: [bold]{valueY}[/] 43_units {name}: [bold]{valueY}[/]";
      series1.tooltip.background.fill = am4core.color("red");
      series1.tooltip.label.textAlign = "middle";
      series1.cursor.maxTooltipDistance = 30;
      series1.tooltip.label.maxWidth = 15;
      series1.tooltip.label.wrap = true;
      series1.fill = am4core.color("red");
      // series1.strokeWidth = 6;
      series1.tooltip.background.propertyFields.stroke = am4core.color("red");
      series1.tooltipText =
        "41_units {name}: [bold]{valueY}[/]  42_units {name}: [bold]{valueY}[/] 43_units {name}: [bold]{valueY}[/]";
      series2 = series1;
      series3 = series1;

      // alert("Selected from " + from + " to " + to);
      console.log("Selected from " + from + " to " + to);
    });

    this.chart = chart;
    console.log("==================|LuskaX2|===================");
    console.log(this.chart);
    console.log(this);
    console.log("==================|LuskaX3|===================");
  },

  beforeUnmount() {
    if (this.chart) {
      this.chart.dispose();
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.hello {
  width: 100%;
  height: 750px;
}
</style>