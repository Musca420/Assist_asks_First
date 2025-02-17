# assist_asks
This is for set it up: a question is asked under a specific condition by satellite. Depending on the question asked, a “Yes” or “No” response will trigger an action.
This all begins by creating two input texts;  input_text.yes_no and input_text.intent_id. The first will be used to write the response, and the second provides a reference for what the response pertains to.

Next, we create a Custom Sentence and an Intent Script. In the Custom Sentence, we write affirmative phrases that are not normally used on their own like “yes”, “ok, fine”, etc. The Intent Script linked to the Custom Sentence does nothing more than write the value “Yes” on input_text.si_o_no, which can be later used in Node-RED or an automation.


HOW TO USE IT:

1) CREATE 2 INPUT TEXT (YOU CAN CREATE IT FROM HELPERS). NAME IT AS input_text.yes_no AND THE SECOND ONE input_text.intent_id
2) COPY THE CONTENT OF "CUSTOM SENTENCE" FOLDER IN: homeassistant/custom_sentence_/en/Answer.yaml
3) COPY THE CONTENT OF INTENT_SCRIPT FOLDER IN YOUR CONFIGURATION.YAML FILE
4) INSTALL "NODE RED" INTEGRATION
   
