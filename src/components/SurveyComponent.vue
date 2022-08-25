<template>
  <h1>Test</h1>
  <div id="surveyCreator" />
</template>

<script>

import { SurveyCreator } from "survey-creator-knockout";
import "survey-core/defaultV2.min.css";
import "survey-creator-core/survey-creator-core.min.css";

const creatorOptions = {
  showLogicTab: true,
  isAutoSave: true
};

const defaultJson = {
  "pages": [
  {
   "name": "Name",
   "elements": [
    {
     "type": "radiogroup",
     "name": "question2",
     "title": "From the information provided (website, brochure), do you understand why GCC is developing these proposals?",
     "choices": [
      {
       "value": "item1",
       "text": "Local resident"
      },
      {
       "value": "item2",
       "text": "Local business"
      },
      {
       "value": "item3",
       "text": "On behalf of a voluntary or community sector organisation"
      },
      {
       "value": "item4",
       "text": "Someone who travels to or through the area from elsewhere"
      },
      {
       "value": "item5",
       "text": "Elected member"
      },
      {
       "value": "item6",
       "text": "District or parish school"
      }
     ]
    },
    {
     "type": "radiogroup",
     "name": "question1",
     "title": "In what capacity are you responding to this survey?",
     "choices": [
      {
       "value": "item1",
       "text": "Fully understand"
      },
      {
       "value": "item2",
       "text": "Partially understand"
      },
      {
       "value": "item3",
       "text": "Don't understand at all"
      }
     ]
    }
   ]
  }
 ]
};

export default {
  name: "survey-creator",
  mounted() {
    const creator = new SurveyCreator(creatorOptions);
    creator.text = window.localStorage.getItem("survey-json") || JSON.stringify(defaultJson);
    creator.saveSurveyFunc = (saveNo, callback) => { 
      window.localStorage.setItem("survey-json", creator.text);
      callback(saveNo, true);
      // saveSurveyJson(
      //     "https://your-web-service.com/",
      //     creator.JSON,
      //     saveNo,
      //     callback
      // );
    };
    creator.render("surveyCreator");
  }
};

// function saveSurveyJson(url, json, saveNo, callback) {
//   const request = new XMLHttpRequest();
//   request.open('POST', url);
//   request.setRequestHeader('Content-Type', 'application/json;charset=UTF-8');
//   request.addEventListener('load', () => {
//       callback(saveNo, true);
//   });
//   request.addEventListener('error', () => {
//       callback(saveNo, false);
//   });
//   request.send(JSON.stringify(json));
// }
// export default {
//   name: 'SurveyComponent',
  
// }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

