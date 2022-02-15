<template>
  <div class="container">
    <!-- If you want to hide survey, comment the lines below -->
    <h2>课程报名</h2>
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
      "progressBarType": "buttons",
      "showProgressBar": "top",
       pages: [
         {
            "navigationTitle": "基本信息",
            "navigationDescription": "课程资料&个人信息",
          questions: [
            {
            "name": "item",
            "type": "text",
            "title": "报名项目",
            "placeHolder": "竞技体操",
            "isRequired": true,
            "autoComplete": "name"
            },
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
            "name": "level",
            "title": "课程级别",
            "isRequired": true,
            "colCount": 0,
            "choices": [
                 "高",
                "中等",
                "低"
                        ]
            }
          ],
        "name": "basciInfo",
        "title": "课程及个人基本信息",
        },
        {
          "navigationTitle": "紧急联系人信息",
          questions: [
            {
            "name": "Ename",
            "type": "text",
            "title": "姓名（中文）",
            "placeHolder": "用户007",
            "isRequired": true,
            "autoComplete": "Ename"
            },
            {
              "name":"tel",
              "type":"text",
              "title":"電話",
              "isRequired": true,
              "autoComplete": "tel"
            },
            {
              "name":"address",
              "type":"text",
              "title":"通訊地址",
              "isRequired": true,
              "autoComplete": "addr"
            }
          ],
        "name": "EmerageInfo",
        "title": "紧急联系人信息",
        },
        {
          "navigationTitle": "缴费方式",
          questions:[
            {
            "type": "radiogroup",
            "name": "paying",
            "title": "繳費方式",
            "isRequired": true,
            "hasNone": false,
            "colCount": 2,
            "choices": [
                "支票（郵寄）",
                "現金（親身遞交）"
            ]
            }
          ],
          "name":"paymentM",
          "title":"缴费方式"
        },
        {
          "navigationTitle": "声明",
          questions:[
            {
           "type": "radiogroup",
            "name": "isOld",
            "title": "你是否已年滿18歲",
            "isRequired": true,
            "hasNone": false,
            "colCount": 2,
            "choices": [
                "未滿18歲由家長填寫",
                "已滿18歲自行填寫"
            ]
            },
            {
              "type":"html",
              "name":"words",
              "html":"<p>謹證明本人是自願參加此課程，並願意自行承擔所有責任。本人亦謹遵守貴會之一切規則、決定，包括藥物檢查條例。本人、本人之繼承人、本人之遺囑執行人及本人之管理人謹此豁免中國香港體操總會、所有贊助商、支持是項活動之團體及任何有關之團體對於本人因參加是項比賽或課程而由任何原因，包括疏忽，所引致之疾病、死亡、個人損失之任何法律責任，以及放棄任何有關之權利、索償及追究行動。本人亦同時聲明本人身體狀況良好及具備足夠之體能及技術完成賽事。本人願意授權大會及傳媒在無須本人審查而可以使用本人的肖像、姓名、聲線及個人資料作為活動籌辦及推廣之用。</p>"
              },
            {
              "type":"html",
              "name":"words2",
              "html":"<p>本人已細閱及明瞭<a href='https://www.google.com/url?q=http://www.gahk.org.hk/doc/Physical%2520Activity%2520Readiness.pdf&sa=D&source=editors&ust=1616178427803000&usg=AFQjCNHF3NxAuur-qus3owpd-rcF6yQUQA' target='_blank'>附件一</a>之體能及健康須知，並同時聲明本人/敝子女身體狀況良好及具備足夠之體能及技術完成賽事或訓練課程。</p>"
            
            },
            {
            "type": "checkbox",
            "name": "isAgree",
            "title": "是否同意上述声明",
            "isRequired": true,
            "hasNone": false,
            "colCount": 1,
            "choices": [
               "同意"
            ]
            },
            {
            "type": "checkbox",
            "name": "isCorrect",
            "title": "請確保所填寫的資料均屬正確",
            "isRequired": true,
            "hasNone": false,
            "colCount": 1,
            "choices": [
               "正確"
            ]
            },


          ],
          "name":"declare",
          "title":"声明"
        }


       ]
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
      // const results = sender.data;

      // let list = localStorage.getItem('apply-course-page-data')

      // if (list) {
      //   list = JSON.parse(list)
      // } else {
      //   list = []
      // }

      // list.push(results)

      // localStorage.setItem('apply-course-page-data', JSON.stringify(list))

       var response = await fetch("http://localhost:1337/student/create", {
              method: "POST",
              body: JSON.stringify(sender.data)
            });

             if (response.ok) {
              var students = await response.text();
              console.log(students)
              // `this` inside methods points to the Vue instance
            } else {
              console.log(response.statusText);
            }
    },
    // async alertResults(sender) {
    //   const results = JSON.stringify(sender.data);

    //   var response = await fetch("https://httpbin.org/post", {
    //     method: "POST",
    //     body: results
    //   });

    //   if (response.ok) {
    //     var persons = await response.text();
    //     alert(persons)
    //     // `this` inside methods points to the Vue instance
    //   } else {
    //     alert(response.statusText);
    //   }
    // },
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
