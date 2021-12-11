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
    chart.paddingRight = 20;
    chart.dateFormatter.inputDateFormat = "yyyy-MM-dd";

    let title = chart.titles.create();
    title.text = "MARVIN FINANCIAL PORTFOLIO, $ZMK";
    title.fontSize = 25;
    title.tooltipText = "Sales in millions of US$ during selected period";

    var dateAxis = chart.xAxes.push(new am4charts.DateAxis());
    dateAxis.renderer.grid.template.location = 0;
    dateAxis.renderer.minGridDistance = 50;
    dateAxis.dateFormats.setKey("day", "dd");
    dateAxis.dateFormats.setKey("week", "dd");
    dateAxis.periodChangeDateFormats.setKey("day", "[bold]MMM");
    dateAxis.periodChangeDateFormats.setKey("week", "[bold]MMM");

    var valueAxis = chart.yAxes.push(new am4charts.ValueAxis());
    valueAxis.tooltip.disabled = true;

    var series = chart.series.push(new am4charts.CandlestickSeries());
    series.dataFields.dateX = "date";
    series.dataFields.valueY = "close";
    series.dataFields.openValueY = "open";
    series.dataFields.lowValueY = "low";
    series.dataFields.highValueY = "high";
    series.simplifiedProcessing = true;
    series.tooltipText =
      "OPEN: [bold]{openValueY}[/]\nHIGH: [bold]{highValueY}[/]\nLOW: [bold]{lowValueY}[/]\nCLOSE: [bold]{closeValueY}[/]\n";

   chart.cursor = new am4charts.XYCursor();

    console.log('SECOND-',chart)

    chart.cursor.behavior = "selectXY";
    chart.cursor.events.on("selectended", function (ev) {
    //chart.cursor = new am4charts.XYCursor();
      let range = ev.target.xRange;
      let axis = ev.target.chart.xAxes.getIndex(0);
      let from = axis.getPositionLabel(axis.toAxisPosition(range.start));
      let to = axis.getPositionLabel(axis.toAxisPosition(range.end));
      series.dataFields.dateX = "date";
      series.dataFields.valueY = "close";
      series.dataFields.openValueY = "open";
      series.dataFields.lowValueY = "low";
      series.dataFields.highValueY = "high";
      series.simplifiedProcessing = true;
      series.tooltipText =
        "OPEN: [bold]{openValueY}[/]\nHIGH: [bold]{highValueY}[/]\nLOW: [bold]{lowValueY}[/]\nCLOSE: [bold]{closeValueY}[/]\n";
      series.tooltip.label.textAlign = "middle";
      chart.tooltip.getFillFromObject = false;
      series.tooltip.background.fill = am4core.color("red");
      series.tooltip.background.propertyFields.stroke = am4core.color("red");
      console.log("Selected from " + from + " to " + to);
    });

    chart.cursor = new am4charts.XYCursor();
    chart.data = [
      {
        date: "2011-09-30",
        open: "154.63",
        high: "157.41",
        low: "152.93",
        close: "156.34",
      },
      {
        date: "2011-10-01",
        open: "156.55",
        high: "158.59",
        low: "155.89",
        close: "158.45",
      },
      {
        date: "2011-10-02",
        open: "157.78",
        high: "159.18",
        low: "157.01",
        close: "157.92",
      },
      {
        date: "2011-10-03",
        open: "158.00",
        high: "158.08",
        low: "153.50",
        close: "156.24",
      },
      {
        date: "2011-10-04",
        open: "158.37",
        high: "161.58",
        low: "157.70",
        close: "161.45",
      },
      {
        date: "2011-10-07",
        open: "163.49",
        high: "167.91",
        low: "162.97",
        close: "167.91",
      },
      {
        date: "2011-10-08",
        open: "170.20",
        high: "171.11",
        low: "166.68",
        close: "167.86",
      },
      {
        date: "2011-10-09",
        open: "167.55",
        high: "167.88",
        low: "165.60",
        close: "166.79",
      },
      {
        date: "2011-10-10",
        open: "169.49",
        high: "171.88",
        low: "153.21",
        close: "162.23",
      },
      {
        date: "2011-10-11",
        open: "163.01",
        high: "167.28",
        low: "161.80",
        close: "167.25",
      },
      {
        date: "2011-10-14",
        open: "167.98",
        high: "169.57",
        low: "163.50",
        close: "166.98",
      },
      {
        date: "2011-10-15",
        open: "165.54",
        high: "170.18",
        low: "165.15",
        close: "169.58",
      },
      {
        date: "2011-10-16",
        open: "172.69",
        high: "173.04",
        low: "169.18",
        close: "172.75",
      },
    ];
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

body {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica,
    Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji", "Segoe UI Symbol";
}

#chartdiv {
  width: 100%;
  height: 1360px;
}
.hello {
  width: 100%;
  height: 750px;
}
</style>
