<template>
  <div>
    <div id="chart" class="chart" />
  </div>
</template>

<script>
import { ref } from 'vue';
import axios from 'axios';
import anychart from 'anychart';

export default {
  data() {
    return {
      option: ref({
        // label: {
        // 	formatter: function (params) {
        // 		return params.name.slice(0, 10) + '…';
        // 	}
        // },
        series: {
          data: [],
        }
      }),
      chart: null,
    };
  },
  methods: {
    setAvatar() {
      let img = '../public/favicon.ico';
      this.chart.center().content(img);
    },
    async fetchData() {
      try {
        const response = await axios.get('URL_FOR_CHARTDATA');
        this.option.series.data = response.data;
      } catch (e) {
        const defaultData = [
          {
            "name": "Management of Companies and Enterprises",
            "children": [
              {
                "name": "Managers, All Other",
                "children": [
                  {
                    "name": "Communication",
                    "value": 1,

                  },
                  {
                    "name": "Active listening",
                    "value": 1

                  },
                  {
                    "name": "Teamwork",
                    "value": 1

                  }
                ]
              },
              {
                "name": "Top Executives",
                "children": [
                  {
                    "name": "Leadership",
                    "value": 1

                  }
                ]
              },
              {
                "name": "Management Occupations",
                "children": [
                  {
                    "name": "Presentation",
                    "value": 1

                  }
                ]
              },
              {
                "name": "Computer and Information Systems Managers",
                "children": [
                  {
                    "name": "Project Planning",
                    "value": 1
                  }
                ]
              }
            ]
          },
          {
            "name": "Information",
            "children": [
              {
                "name": "Software Developers and Programmers",
                "children": [
                  {
                    "name": "Software Configuration Management",
                    "value": 1
                  },
                  {
                    "name": "Software Engineering",
                    "value": 1
                  },
                  {
                    "name": "Python",
                    "value": 1
                  },
                  {
                    "name": "Hypertext Markup Language",
                    "value": 1
                  },
                  {
                    "name": "C#",
                    "value": 1
                  }
                ]
              },
              {
                "name": "Computer Network Architects",
                "children": [
                  {
                    "name": "Wireless Sensor Network",
                    "value": 1
                  },
                  {
                    "name": "Telecommunications Network",
                    "value": 1
                  },
                  {
                    "name": "Network Infrastructure",
                    "value": 1
                  },
                  {
                    "name": "Wireless LAN",
                    "value": 1

                  },
                  {
                    "name": "Computer Security",
                    "value": 1

                  },
                  {
                    "name": "Software Defined Networking",
                    "value": 1

                  }
                ]
              },
              {
                "name": "Computer and Information Analysts",
                "children": [
                  {
                    "name": "Software Optimization",
                    "value": 1

                  }
                ]
              },
              {
                "name": "Software Developers, Applications",
                "children": [
                  {
                    "name": "Computer Program",
                    "value": 1

                  }
                ]
              }
            ]
          },
          {
            "name": "Administrative and Support and Waste Management and Remediation Services",
            "children": [
              {
                "name": "Document Preparation Services",
                "children": [
                  {
                    "name": "LaTeX Software",
                    "value": 1

                  }
                ]
              }
            ]
          }
        ];
        this.option.series.data = defaultData;
      }

      this.chart = anychart.sunburst(this.option.series.data, "as-tree");
      this.chart.container("chart");
      this.chart.calculationMode('parent-independent');
      this.chart.sort('asc');

      //this.setAvatar('../public/favicon.ico');
      this.chart.draw();
    },
    loadChartAndDraw() {
      const script1 = document.createElement('script');
      script1.src = 'https://cdn.anychart.com/releases/8.11.1/js/anychart-core.min.js';
      document.head.appendChild(script1);

      const script2 = document.createElement('script');
      script2.src = 'https://cdn.anychart.com/releases/8.11.1/js/anychart-sunburst.min.js';
      document.head.appendChild(script2);

      const script3 = document.createElement('script');
      script3.src = 'https://cdn.anychart.com/releases/8.11.1/js/anychart-sunburst.min.js';
      document.head.appendChild(script3);

      script3.onload = () => {
        this.fetchData();
      };
    }
  },
  mounted() {
    const script = document.createElement('script');
    script.src = 'https://cdn.anychart.com/releases/8.11.1/js/anychart-core.min.js';
    document.head.appendChild(script);
    script.src = 'https://cdn.anychart.com/releases/8.11.1/js/anychart-sunburst.min.js';
    document.head.appendChild(script);

    this.loadChartAndDraw();
  },
};
</script>


<style>
html,
body {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
}

label {
  display: inline-block;
  margin: 10px 0 0 10px;
}

#chart {
  position: absolute;
  width: 100%;
  top: 35px;
  bottom: 0;
}
</style>
