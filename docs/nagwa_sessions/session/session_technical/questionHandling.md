# Handling Questions Sharing & Answering

One of the main features of the HTML rendering engine is the ability to render questions and support answering them. Once the educator starts a question, the student can answer it in real time, and the answer will be shared with the educator.

## Questions Asking Status

### Inital Status

The question is considered Initial when an educator selects a question slide but has not yet started it,  In this case, the question will be shared with students, but they will not be able to answer it. The educator can change the question-asking status at any time by clicking on the question icon.

??? example "Question Initial Status - Student View "
    <iframe frameborder="0" style="width:100%;height:392px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1jVNXHGA6_agZFjfpN_448ML-6izXbZL4"></iframe>

??? example "Question Initial Status - Educator View "
    <iframe frameborder="0" style="width:100%;height:510px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G18rjJyOP0xzE5iZXfsHMcbHJ9axtZwwTm"></iframe>

### In-Progress Status

This is the status that happens when an educator starts a question and students can respond. Students choose their answer and press "send." Once submitted, the educator views student responses. Students can't change their answers. Eventually, the right answer is revealed.

- Wrong Answer: If a student's response is wrong, their choice turns red. The correct answer becomes green.
- Correct Answer: If a student's response is correct, their choice turns green.

!!! note "In `in_progress` status, the students can scroll the question as they need, the scroll is done on their local device and doesn’t affect the remaining participant's"

??? example "Question In_Progress Status - Educator View "
    <iframe frameborder="0" style="width:100%;height:577px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1MBDedZtXAvabbEbtoHIQWlh5aT37aikv"></iframe>

??? example "Answered Question - Student View "
    <iframe frameborder="0" style="width:100%;height:462px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1sN3sV1vvv1Y9HOYNwOdHWon1tBO-nXuQ"></iframe>

### Time_Is_Up Status

This is the status of a question when the educator has stopped students from answering. This will end the question for all students. All students will be able to see the questions insights, which vary based on the question type:

- In the case of MCQ Questions, it will show each answer choice and the total number of students who selected that choice.

- In the case of questions that require text answer, it will show every student's answer in a single box

??? example "Change status to Time_Is_Up  - Educator View "
    <iframe frameborder="0" style="width:100%;height:672px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G14Mm0vuA_C79irjyF8L-UXusJ3vDW5vz5"></iframe>

!!! info "When the educator press the ‘time_is_up’ button, we will share all answers with all students in the session, To stop the insights sharing, the educator needs to press the done button, which will restore the question asking status to initial"

??? example " Stop Sharing Answers and Insights With Students"
    <iframe frameborder="0" style="width:100%;height:491px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1p8ViPgWSwJww23WhWynTGTTpiaOOwrBp"></iframe>

---------------------

## Updating the Question Asking Status

To send an update to the students that the question status [Initial, In_Progress, Time_Is_Up] has been changed, the `updateQuestionAskingStatus` method is called when the educator clicks on the question button in the WebView. This function allows you to control the time-limited behavior of the application as required. as it calls the update question function from the html rendering engine
`NagwaRenderingEngine.updateCurrentQuestionAskingStatus($questionAskingStatus);`

!!! note "For more information , kindly navigate to [`updateCurrentQuestionAskingStatus` section](../../pre_knowledge_required/js_html_renderingEngine.md/?h=updatecurrentquestionaskingstatus#updatechatstatusstatus)"

!!! info "Keep In Mind"
    - When “CurrentQuestionAskingStatus” is set to “In_Progress”, the student will be able to scroll and submit the question answer once.
    <br>
    - When current_question_asking_status is set to “Time_Is_Up”, the student won't be able to scroll or submit the answer anymore, indicating that the time limit for the activity has expired.
-----------------------

## Receiving Questions Status Update

The HTML rendering engine will fire a `questionAskingStatusUpdated` event when the `questionAskingStatus` is updated, for that we use a  questionAskingStatusUpdated function which handle it and emits QuestionAskingStatusChanged state.

------

## Handling Answer's Insights
When the educator changes the question-answering status to be `Time_Is_Up`, a question insight will be shared with all students, in this case, an `interactionUpdated` event will be fired, For that, we are using the `getInsights` which is a callback function that is called when the insights are updated in the WebView.

!!! infor "Answer insights will be shared with all session students, including those who didn’t answer the question."


??? quote "Output object if the question type is `aggregated_all_possible_answers` or `aggregated_only_student_answers`"
    ```json
    {
    "currentScreen": "4",
    "questionID": "245178050680.2",
    "questionType": "aggregated_all_possible_answers",
    "choices": ["أ", "ب", "ج", "د"],
    "totalInteractions": 1,
    "interactions": {
        "أ": {
            "count": 1,
            "percentage": 100,
            "answer": "أ"
        },
        "ب": {
            "count": 0,
            "percentage": 0,
            "answer": "ب"
        },
        "ج": {
            "count": 0,
            "percentage": 0,
            "answer": "ج"
        },
        "د": {
            "count": 0,
            "percentage": 0,
            "answer": "د"
        }
    },
    "correctAnswers": [], // always empty array
    "currentStudentAnswer: "أ", // or null if the student didn't answer
    "messageKey": "interactionUpdated"
    }
    ```



### Handling Insight data recived using the `getInsights` function?

1. Clear the answers list and the answersStatistic map and set the isThereActiveQuestion, isAnswered, and isDisabled to false.
2. Parses the JSON string that is passed from the WebView to a map
3. Gets the “questionID”  from the map, which is the current question selected by the educator
4. Gets the questionType from the map which is the type of the question, it can be 
      1. aggregated_all_possible_answers
      2. aggregated_only_student_answers
      3. Separated
5. Gets the screenId from the map, which is the current screen (slide) that the educator is in and sharing 
6. Get the totalInteractions which is the total question answer.
7. Gets the interactions, which is a map that contains:
      1. Count
      2. Percentage
      3. Timestamp
      4. Answer  
      5. studentName
8. Then it iterates over the interactions map and for each answer, it takes the count, percentage, timestamp, answer, and studentName from the answer object 
9. Check if the questionType is separated or not and then add the answer to the answersStatistic map with the answer as a key and a StatisticEntity as a value 
10. Emits a QuestionGotten state



#### Questions Types
<table style="border-collapse: collapse; width: 100%; margin: 0 auto;">
    <tr>
        <th style="text-align: left; padding: 10px;">Question Type</th>
        <th style="text-align: left; padding: 10px;">Description</th>
    </tr>
    <tr>
        <td style="text-align: left; padding: 10px;">Aggregated_all_possible_answers</td>
        <td style="text-align: left; padding: 10px;">This type is for multiple-choice questions (MCQs), where all the answer options are displayed, along with the percentage of students who selected each option in the insights.</td>
    </tr>
    <tr>
        <td style="text-align: left; padding: 10px;">Aggregated_only_student_answers</td>
        <td style="text-align: left; padding: 10px;">This type is for multiple-response questions (MRQs), where students can choose more than one answer. For example, if students choose options "ab," "ac," and "cd," only these selected choices are shown in the insights. If no students select an option like "bd," it won't appear in the insights.</td>
    </tr>
    <tr>
        <td style="text-align: left; padding: 10px;">Separated</td>
        <td style="text-align: left; padding: 10px;">This type is for questions with input boxes, where students provide text-based answers. All the submitted answers are displayed in the insights.</td>
    </tr>
</table>






??? example "Questions Insights Types"
    <iframe frameborder="0" style="width:100%;height:458px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1B-sEyR-Wr3iNVHRdsf8X9ZopOoIeDag_"></iframe>


!!! note "`getInsights` path : [lib/features/sessions/presentation/logic/engagement/engagement_cubit.dart](https://dev.azure.com/nagwa-limited/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/features/sessions/presentation/logic/engagement/engagement_cubit.dart&version=GBdevelopment)"

## Counting Number of Students Who Didn’t Answer Yet
In order to display the number of students who haven’t answered yet, we have developed a function `getRemainingStudents` that checks if the number of answered students is greater than the number of online students and returns 0. Otherwise, it returns the difference between the number of online students and the number of answered students 

??? example "Counting Number of Students Who Didn’t Answer Yet"
    <iframe frameborder="0" style="width:100%;height:341px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G10ZFD1vcf13TSfX68gCDc1uteu3Ej1szz"></iframe>