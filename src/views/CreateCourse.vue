<template>
  <div class="container">
    <!-- If you want to hide survey, comment the lines below -->
    <h2>创建课程</h2>
    <survey :survey="survey"></survey>
  </div>
</template>

<script>
import * as SurveyVue from "survey-vue";
import "bootstrap/dist/css/bootstrap.css";
var Survey = SurveyVue.Survey;
Survey.cssType = "bootstrap";

import * as widgets from "surveyjs-widgets";

import { init as customWidget } from "../components/customwidget";

// widgets.icheck(SurveyVue);
widgets.select2(SurveyVue);
widgets.inputmask(SurveyVue);
widgets.jquerybarrating(SurveyVue);
widgets.jqueryuidatepicker(SurveyVue);
widgets.nouislider(SurveyVue);
widgets.select2tagbox(SurveyVue);
widgets.sortablejs(SurveyVue);
widgets.ckeditor(SurveyVue);
widgets.autocomplete(SurveyVue);
widgets.bootstrapslider(SurveyVue);
customWidget(SurveyVue);

SurveyVue.Serializer.addProperty("question", "tag:number");

export default {
  components: {
    Survey
  },
  data() {
    var json = {
      pages: [
         {
          questions: [
            {
            "name": "code",
            "type": "text",
            "title": "课程编码",
            "placeHolder": "A000007",
            "isRequired": true,
            "autoComplete": "code"
            },
            {
            "type": "dropdown",
            "name": "category",
            "title": "体操类别",
            "isRequired": true,
            "colCount": 0,
            "hasNone": true,
            "choices": [
                "鞍马",
                "平衡木",
                "蹦床",
                "高低杠"
            ]
            },
            {
            "type": "dropdown",
            "name": "difficulty",
            "title": "项目难度",
            "isRequired": true,
            "colCount": 0,
            "hasNone": true,
            "choices": [
                "高",
                "中等",
                "低"
            ]
            },
            {
            "type": "dropdown",
            "name": "coach",
            "title": "教练",
            "isRequired": true,
            "colCount": 0,
            "hasNone": true,
            "choices": [
                "Bob",
                "Cindy",
                "Jack"
            ]
            },
            {
              "type": "text",
              "name": "Sdate",
              "title": "开始日期",
              "inputType": "date"
            },
            {
              "type": "text",
              "name": "Edate",
              "title": "结束日期",
              "inputType": "date"
            },
            {
            "type": "checkbox",
            "name": "week",
            "title": "星期 ",
            "isRequired": true,
            "colCount": 1,
            "choices": [
               "一",
               "二",
               "三",
               "四",
               "五",
               "六",
               "日",
            ]
            },
            {
            "type": "comment",
            "name": "dates",
            "title": "所有上课日期",
            },
            {
              "type": "text",
              "name": "Ddate",
              "title": "截止日期",
              "inputType": "date"
            },
            {
            "name": "time",
            "type": "text",
            "title": "截止时间",
            "isRequired": true,
            "autoComplete": "time"
            },
            {
            "name": "Uage",
            "type": "text",
            "title": "年龄上限",
            "isRequired": true,
            "autoComplete": "Uage"
            },
            {
            "name": "Lage",
            "type": "text",
            "title": "年龄下限",
            "isRequired": true,
            "autoComplete": "Lage"
            },
            {
            "type": "dropdown",
            "name": "gym",
            "title": "体育馆",
            "isRequired": true,
            "colCount": 0,
            "hasNone": true,
            "choices": [
                "体育馆1号",
                "体育馆2号",
                "体育馆3号"
            ]
            },
            {
            "type": "dropdown",
            "name": "gym",
            "title": "场地",
            "isRequired": true,
            "colCount": 0,
            "hasNone": true,
            "choices": [
                "蹦床馆",
                "单杠馆",
                "训练室"
            ]
            },
            {
            "name": "quato",
            "type": "text",
            "title": "名额",
            "isRequired": true,
            "autoComplete": "quato"
            },
            {
            "name": "fee",
            "type": "text",
            "title": "费用",
            "isRequired": true,
            "autoComplete": ""
            },
            {
            "type": "intro",
            "name": "dates",
            "title": "内文",
            },


          ],
      }      
       ]
    };
    var model = new SurveyVue.Model(json);
    model.onComplete.add(this.alertResults);
    return {
      survey: model
    };
  },
  methods: {
    async alertResults(sender) {
      const results = JSON.stringify(sender.data);
      alert(results);
      var response = await fetch("https://httpbin.org/post", {
        method: "POST",
        body: JSON.stringify(sender.data)
      });
      if (response.ok) {
        var persons = await response.text();
        alert(persons)
        // `this` inside methods points to the Vue instance
      } else {
        alert(response.statusText);
      }
    },
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
