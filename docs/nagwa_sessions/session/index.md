# Session Feature

!!! tip " It’s Highly recommended to have a look at the [Pre-Knowledge Required Before Technical Dealing With Sessions](../pre_knowledge_required/index.md) section before diving deep into the session feature."

## Business Overview

### Session Listing

Educators have a central place where they can easily see all their ongoing and upcoming sessions. This list shows when each session will happen, how long it will be, and how many students enrolled in the session class.

- Date and Duration: The educator can see exactly when each session will start and how long each session is supposed to last.
  
- Subject: The topic or subject of each session
  
- Number of Students: number of class students who are expected to attend the session
  
- Action Button: When it's time for a session to begin, there's a start button that the educator can press.
  
### Session Starting

Once session time is reached, the session action card becomes active and clickable, and the educator can click start Then it will be available for students to join

### Session Cancellation ❌

The educator can cancel the session anytime before it starts, Once cancelled it will be removed from the student’s session list

### Session Control Features

- **Mute/Un-Mute Mic**: The educator can turn their microphone on and off as needed.
- **End Session**: The educator has the ability to end the session at any time, which will result in all students being kicked out .
- **View Students List**: Educators can see a list of current online students who are attending the session.
- **Allowing Students to Speak**: When a student raises their hand, the educator can permit them to speak. After they're done, the educator can take away the speaking permission, muting the student again.
- **Kickout Student**: Educators can (block) remove a student from the meeting, preventing them from rejoining the session.
- **Enable/Disable Chat**: Educators can decide whether to let students use text chat during the session.

### Live Drawing Sharing

The educator can draw on the screen, and these drawings will be instantly visible to the students. **This feature currently supports drawing with an Apple Pencil**, here is all available drawing Options

#### Pen Selection

The educator can choose a pen and pick a color from various color choices. They can also adjust the thickness of the lines.

#### Erasing Options

The educator has multiple ways to erase:

- **Pen Eraser**: This special pen, colored white, removes text or drawings by covering them with white.
  
- **Object Eraser**: It selectively erases certain objects or connected lines. Clicking on any part of an object will erase it.
  
- **Reset Button**: This resets the entire screen to its original state, removing all drawings and returning it to default.

### Live Questions Sharing

Educators can share questions with students in real time. Students can submit their answers, which are then immediately visible to the educator. The educator can review the answers and share insights when the designated time is reached. Students have various ways to respond based on the question type.

- When the educator selects a question slide, the question is displayed for students. However, students cannot respond at this point.
  
- Once the educator starts the question, students can submit their answers based on question type and click the submit button. At this point, Students can scroll through the question if needed. Each student can submit their answer only once.

- When the educator clicks the "Time is Up" button, students cannot submit further answers. They can now gain insights from the answers provided by their peers.

- Clicking the "Done" button by the educator removes the answer insights from the students' view.

### Adding Empty Slides

Educators have the option to add empty slides if they want to demonstrate more ideas and need more drawing space

### Communication Channals

#### Voice Communication

The educator can use voice communication to interact with students,he can grant/revok speaking student permission to speak when needed

#### Text Chat

Students can send text messages in the chat, which can be read by the instructor. However, the instructor cannot reply and he only have the option to read the messages or even disable the text chat functionality for students.

### Internet Connection Handling

When internet connection issues occur from the educator's side, The system will instantly notify him regarding the issue, and we’ll retry to connect him again while he is still on the session screen.

---------------------------------

### Supported Question Types

<table width="100%" style="border-collapse: collapse;">
    <tr>
        <th style="width: 20%; text-align: left;">Question Type</th>
        <th style="width: 80%; text-align: left;">Description</th>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">Free Response Question (FRQ)</td>
        <td style="width: 80%; text-align: left;">If the question requires a text-based response, students can type their answers as text and submit them. These answers will be shared with the educator.</td>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">Multiple-Choice Questions (MCQ)</td>
        <td style="width: 80%; text-align: left;">If the question is in multiple-choice format, students can select the answer and submit it. After submitting, they can view the answers chosen by their peers.</td>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">True/False Questions</td>
        <td style="width: 80%; text-align: left;">If the question to answer is in a true or false format, students can select the correct answer and submit it. After submitting, the answer will be shared with the educator.</td>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">Input Box Questions (IBQ)</td>
        <td style="width: 80%; text-align: left;">In this type, we limit the student to provide a single type of answer. For example, if it's a math question and the answer should be an integer number, the student will not be allowed to submit a double number or character-based answer. Only numerical integer answers will be accepted.</td>
    </tr>
    <tr>
        <td style="width: 20%; text-align: left;">General Multiple Response Questions (GMRQ)</td>
        <td style="width: 80%; text-align: left;">These questions emulate a matching-style format where students are presented with two columns. They must match the items in the first column with their corresponding elements in the second column correctly.</td>
    </tr>
</table>
