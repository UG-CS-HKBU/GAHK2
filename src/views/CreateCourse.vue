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
    Survey,
  },
  data() {
    var json = {
      pages: [
        {
          questions: [
            {
              name: "code",
              type: "text",
              title: "課程編碼",
              placeHolder: "A000007",
              isRequired: true,
              autoComplete: "code",
            },
            {
              type: "dropdown",
              name: "category",
              title: "體操類別",
              isRequired: true,
              colCount: 0,
              hasNone: true,
              choices: ["競技體操", "藝術體操", "技巧體操", "彈網", "健美體操", "普及體操", "跑酷"],
            },
            {
              type: "dropdown",
              name: "difficulty",
              title: "項目難度",
              isRequired: false,
              colCount: 0,
              choices: ["高", "中等", "低"],
            },
            {
              type: "dropdown",
              name: "coach",
              title: "教練",
              isRequired: false,
              colCount: 0,
              hasNone: true,
              choices: ["Bob", "Cindy", "Jack"],
            },
            {
              type: "multipletext",
              name: "dates",
              title: "日期",
              isRequired: true,
              colCount: 3,
              validators: [
                {
                  type: "expression",
                  expression:
                    "{dates.Sdate} <= {dates.Edate} and {dates.Sdate} >= {dates.Ddate}",
                  text: "Please correct the date.",
                },
              ],
              items: [
                {
                  name: "Sdate",
                  title: "開始日期",
                  inputType: "date",
                },
                {
                  name: "Edate",
                  title: "結束日期",
                  inputType: "date",
                },
                {
                  name: "Ddate",
                  title: "截止日期",
                  inputType: "date",
                },
              ],
            },
            {
              type: "checkbox",
              name: "week",
              title: "星期 ",
              colCount: 1,
              choices: ["一", "二", "三", "四", "五", "六", "日"],
            },
            {
              type: "comment",
              name: "Alldates",
              title: "所有上課日期",
            },
            {
              name: "time",
              type: "text",
              title: "截止時間",
              isRequred: false,             
            },
            {
              type: "multipletext",
              name: "ages",
              title:"年齡限制",
              isRequired: true,
              colCount: 2,
              validators: [
                {
                  type: "expression",
                  expression: "{ages.Uage} >= {ages.Lage}",
                  text:
                    "Please correct the age. The first value should be large or equal to the second one.",
                },
              ],
              items: [
                {
                  name: "Uage",
                  title: "年齡上限",
                  validators: [
                    {
                      type: "numeric",
                      maxValue: 99,
                    },
                  ],
                },
                {
                  name: "Lage",
                  title: "年齡下限",
                  validators: [
                    {
                      type: "numeric",
                      minValue: 1,
                    },
                  ],
                },
              ],
            },
            {
              type: "dropdown",
              name: "gym",
              title: "體育館",
              isRequired: true,
              colCount: 0,
              hasNone: true,
              choices: ["體育館1號", "體育館2號", "體育館3號"],
            },
            {
              type: "dropdown",
              name: "gym1",
              title: "場地",
              colCount: 0,
              hasNone: true,
              choices: ["蹦床館", "單鋼館", "訓練室"],
            },
            {
              name: "quato",
              type: "text",
              title: "名額",
              isRequired: true,
              autoComplete: "quato",
              validators: [
                {
                  type: "expression",
                  text: "The quato should not less than 1.",
                  expression: "{quato} >= 1",
                },
              ],
            },
            {
              name: "fee",
              type: "text",
              title: "費用",
              isRequired: true,
              validators: [
                {
                  type: "numeric",
                  minValue: 0,
                },
              ],
            },
            {
              type: "comment",
              name: "intro",
              title: "內文",
            },
          ],
        },
      ],
    };
    var model = new SurveyVue.Model(json);
    model.showPreviewBeforeComplete = "showAnsweredQuestions";
    model.onComplete.add(this.alertResults);
    return {
      survey: model,
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
        body: JSON.stringify(sender.data),
      });

      if (response.ok) {
        var courses = await response.text();
        console.log(courses);
        // `this` inside methods points to the Vue instance
      } else {
        console.log(response.statusText);
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
