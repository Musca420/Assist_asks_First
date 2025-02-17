# Assist asks a Question, depends of the question and of our answer, an action will be trigger
This is for set it up: a question is asked under a specific condition by satellite. Depending on the question asked, a “Yes” or “No” response will trigger an action.
This all begins by creating two input texts;  input_text.yes_no and input_text.intent_id. The first will be used to write the response, and the second provides a reference for what the response pertains to.

Next, we create a Custom Sentence and an Intent Script. In the Custom Sentence, we write affirmative phrases that are not normally used on their own like “yes”, “ok, fine”, etc. The Intent Script linked to the Custom Sentence does nothing more than write the value “Yes” on input_text.yes_no, which can be later used in Node-RED or an automation.


HOW TO USE IT:

1) CREATE 2 INPUT TEXT (YOU CAN CREATE IT FROM HELPERS). NAME IT AS input_text.yes_no AND THE SECOND ONE input_text.intent_id
2) UPLOAD Answer.yaml in : homeassistant/custom_sentence/en/ (if you don't have, create those folders)
3) COPY THE CONTENT OF INTENT_SCRIPT FOLDER IN YOUR CONFIGURATION.YAML FILE
4) REBOOT HOME ASSISTANT
5) INSTALL "NODE RED" INTEGRATION
6) DOWNLOAD Flow.json REPOSITORY (YOU NEED IT TO IMPORT THE FLOW OF NODE RED)
7) IN NODE RED GO TO RIGHT ANGLE (THREE LINES), SELECT IMPORT, AND JUST SELECT THE FILE Flow.json
8) NOW YOU HAVE THE FOLOW IMPORT. NOW WE NEED TO SET IT UP 

IN NODE RED THE FLOW IS DIVEDED IN 2 PARTS: 
1) A QUESTION IS ASKED UNDER SPECIFIC CONDITION
2) DEPENDIG OF THE QUESTION, "YES" ANSWER WILL BE TRIGGER AN ACTION

FIRST PART

SO SET UP:
1) "EVENT STATE" CONDITION AND IF YOU WANT PUT MORE CONDITION (EXAMPLE TV ON, MORE CONDITION: WAITING UNTIL light ON)
2) "Set Id intent to action" SELECT ENTITY input_text.intent_id AND ON DATA PUT {   "value": "Your action" } (CHANGE YOUR ACTION TO SET AN EVENT LIKE EXAMPLE: Blinds) {   "value": "Blinds" }
3) ""ASKING" THAT START A tts.cloud_say ACTION, CHANGE DATA WITH {   "cache": false,   "entity_id": "YOUR ASSIST SATELLITE ENTITY",   "message": "WHAT YOU WANT ASSIST ASKS" } LIKE {   "cache": false,   "entity_id": "YOUR ASSIST SATELLITE ENTITY",   "message": "Do you want to close the blinds?" }
4) "set intent id Unknow" CHANGE THE ENTITY input_text.intent_id AND SET THE CONTENT OF DATA {   "value": "Unknow" } (THIS WILL RESET THE INTENT ID TO BE READY TO OTHER AUTOMATION BASED ON THIS METHOD)


SECOND PART

SET UP:
1) "Answer: Yes" SELECT ENTITY input_text.yes_no AND THE CONDITION MUST BE "IF STATE IS : Yes"
2) "set answer to unknow" (THIS WILL RESET, AFTER 20 SEC. THE ANSWER TO "Unknow" TO BE READY TO OTHER AUTOMATION BASED ON THIS METHOD)
3) "intent" THAT IS A CURRENT STATE NODE, JUST SELECT THE ENTITY input_text.intent_id AND LEAVE BLANK THE CONDITION "IF STATE IS" ( THIS WILL BE REPORT US EVERY CURRENT STATE OF  input_text.intent_id ).
4) "Which intentent?" THIS IS A SWITCH NODE, PUT THE SAME NAME OF WHAT YOU PUT IN YOUR ACTION (FIRST PART POINT 2) (IN MY EXAMPLE WE PUT EXACTLY Blinds
5) "select your action" JUST TYPE THE ACTION YOU WANT TO HAPPEN. (IN THIS EXAMPLE WE WILL SELECT COVER OPEN AND AS ENTITY, MY COVER) 

DEPLOY AND NOW THAT IS HOW IT IS WORK:

If I turn on the TV and turn on the light, the STT (speech-to-text) kicks in asking, “Do you want me to close the blind?” (it will write ‘Blinds’ in input_text.id_intent). 
When I Answer “OK Nabu, that’s fine,” te value ‘yes’ is written to input_text.yes_no and it’s linked via a switch node to the intent ID in input_text.id_intent. If ‘Yes’ is linked to an intent ID, the action will be executed and the values will be reset to Unknown. So, the sequence will be: turn on the TV(OR WHAT YOU WANT), turning on the tv (OR WHAT YOU WANT), Satellite will ask, “Do you want  to lower the blind?” I respond “OK Nabu, that’s fine,” and the blind lowers. If desired, another confirmation phrase can be added either with STT or using google_generative_ai_conversation.generate_content for a more colorful sentence.

