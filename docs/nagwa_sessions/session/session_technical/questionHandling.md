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