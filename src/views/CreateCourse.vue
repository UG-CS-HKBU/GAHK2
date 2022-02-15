<template>
  <div class="container">
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
            pages: [{
                questions: [{
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
                        "isRequired": false,
                        "colCount": 0,
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
                        "isRequired": false,
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
                        "isRequired": true,
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
                        "isRequired": true,
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
                        "autoComplete": "Uage"
                    },
                    {
                        "name": "Lage",
                        "type": "text",
                        "title": "年龄下限",
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
                        "name": "gym1",
                        "title": "场地",
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
                        "type": "comment",
                        "name": "intro",
                        "title": "内文",
                    },
                ],
            }]
        };
         var model = new SurveyVue.Model(json);
         model.showPreviewBeforeComplete = 'showAnsweredQuestions';
         model.onComplete.add(this.alertResults);
        return {
            survey: model
        };
    },
    methods: {
        async alertResults(sender) {
            // const results2 = sender.data;

            // let list2 = localStorage.getItem('create-course-page-data')

            // if (list2) {
            //     list2 = JSON.parse(list2)
            // } else {
            //     list2 = []
            // }

            // list2.push(results2)

            // localStorage.setItem('create-course-page-data', JSON.stringify(list2))

            // fetchData: async function () {
            var response = await fetch("http://localhost:1337/course/create", {
              method: "POST",
              body: JSON.stringify(sender.data)

            });

            if (response.ok) {
              var courses = await response.text();
              console.log(courses)
              // `this` inside methods points to the Vue instance
            } else {
              console.log(response.statusText);
            }
        },
    }
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
