# HTML Rendering Engine

The Rendering Engine is a powerful tool that enables the creation and display of drawings, visualizations, activities, and questions. The engine is used with the "Nagwa Classes" app to support the "session" feature.

## Key Features of the HTML Rendering Engine

-   Draw using different colors and sizes with easy-to-use tools.
-   Easily undo or redo changes to perfect your creations.
-   Quickly clear the canvas for a fresh start.
-   Engage users with interactive questions with Question Engine Support.
-   Keep the audience interaction with exciting activities supported by the Activities Engine.
-   Keep data in sync with Firebase for real-time collaboration and accessibility.

## Main Technologies

-   [React](https://reactjs.org/): The foundation of the Rendering Engine, providing a dynamic user interface.
-   [Redux Toolkit](https://redux-toolkit.js.org/): Empowers efficient state management for a smooth user experience.
-   [Firebase](https://firebase.google.com/): Enables real-time data synchronization and storage in the cloud.
-   [Wepack](https://webpack.js.org/): Bundles and optimizes the application for improved performance.
-   [Babel](https://babeljs.io/): toolchain that is mainly used to convert ECMAScript 2015+ code into a backwards compatible version of JavaScript in current and older browsers or environments


## List of Our S3 Buckets

-   [nagwa-sessions-dev](https://s3.console.aws.amazon.com/s3/buckets/nagwa-sessions-dev?region=us-east-1) for the beta engine build
-   [nagwa-sessions-prod](https://s3.console.aws.amazon.com/s3/buckets/nagwa-sessions-prod?region=us-east-1&tab=objects) for the production engine build
-   [visualizations.nagwa.com/rendering-engine-packages](https://s3.console.aws.amazon.com/s3/buckets/visualizations.nagwa.com?region=us-east-1&prefix=rendering-engine-packages/&showversions=false) for the engine package
-   [visualizations.nagwa.com/rendering-engine](https://s3.console.aws.amazon.com/s3/buckets/visualizations.nagwa.com?region=us-east-1&prefix=rendering-engine/&showversions=false) for the demo app

## How to use the engine

### Initialization

In the following example, you will find a code snippet that initializes the rendering engine to establish a connection with the session Firestore and retrieve all the necessary data. Additionally, you'll download the session package to initiate your session smoothly.

```js
window.NagwaRenderingEngine.init({
    name: 'Mohamed Ahmed Mahmoud',
    role: 'educator', // the role of the current user to preview whether `educator` or `student`
    rootElementID: 'root', // the id of the root element to render the engine inside it and if not passed it will be `root`
    userID: '', // the current user id
    sessionID: '347817452421322', // the current session id
    packageBasePath: '/347817452421322', // the base path of the package to download the package
    enginesBasePath: '/engines_base_path', // the base path of the engines
    firebaseConfig: {
        apiKey: 'API KEY',
        authDomain: 'AUTH DOMAIN',
        projectId: 'PROJECT ID',
        storageBucket: 'STORAGE BUCKET',
        messagingSenderId: 'MESSAGING SENDER ID',
        appId: 'APP ID',
    },
});
```

## Engine API

### updateScreen(screenID)

You need to call this function if you want to update the currently active screen and ensure that the changes are also updated in Firebase.

```js
NagwaRenderingEngine.updateScreen('SCREEN_ID');
```

### changeTool(tool)

To update the currently active tool or pen with a new color, size, or type and start using it inside the app view, call this function. The function takes an object as a parameter that may contain any of these three properties:

-   `color`: pass a string with the color of the pen you want to apply.
-   `strokeWidth`:pass a number the with stroke size of the pen you want to apply.
-   `type`: pass the type of pen you need whether `Draw`, `DeletePart`, or `Normal`.

**Note**: To update the pen color, you can call the `changeTool` function with an object that has the color property, whether it's specified as a hexadecimal value or a color name.

```js
NagwaRenderingEngine.changeTool({ color: 'red' });
```

```js
NagwaRenderingEngine.changeTool({ color: '#a83232' });
```

**Note**: To update the pen size (stroke), you can call the `changeTool` function with an object that has the `strokeWidth` property.

```js
NagwaRenderingEngine.changeTool({ strokeWidth: 3 });
```

**Note**: To update the pen type, you can call the `changeTool` function with an object that has the type property. The `type` property should be set to one of the three values:

-   `Draw`: For the draw pen type.
-   `DeletePart`: For the erase object pen type used to delete entire paths or objects.
-   `Normal`: For the normal pen mode, where you can have your default cursor and perform regular actions like clicking to solve a question.

Here's an example snippet that demonstrates how to switch to erase object mode (delete mode) for deleting paths using the `changeTool` function

```js
NagwaRenderingEngine.changeTool({ type: 'DeletePart' });
```

You have the option to send multiple properties at the same time as follows:

```js
NagwaRenderingEngine.changeTool({
    color: 'red',
    strokeWidth: 3,
});
```

### undo()

The undo() function allows you to perform an undo action for your last action and remove it. Within the application, we maintain an undo stack that keeps track of all user actions during the current session, enabling you to perform multiple undo actions as needed. By calling the undo() function, you can effortlessly revert the most recent action and continue undoing previous actions if necessary.

```js
NagwaRenderingEngine.undo();
```

### redo()

The redo() function enables you to redo your last undo action and retrieve it. With the help of our redo stack, which tracks all your undo actions during the current session, you can perform multiple redo actions as needed. Restoring changes that were previously undone becomes effortless,

```js
NagwaRenderingEngine.redo();
```

### Handling Redo and Undo Stack Empty Status

In addition to the `undo()` and `redo()` functions, The engine fires a message to notify you when the undo or redo stack becomes empty. These messages trigger the `historyStatusUpdated` event, allowing you to update your view accordingly. For more detailed information on how to handle these events, please refer to the events section.

### clearScreen()

To clear the entire current screen view, simply call the `clearScreen()` function.
Important to note that executing this action will remove all content, including drawings and images, from the current screen. Keep in mind that this action is irreversible, and you won't be able to undo it. However, the data will be saved inside Firebase, preserving the previous state of your work. Exercise caution when using this function to avoid accidental loss of data.

```js
NagwaRenderingEngine.clearScreen();
```

### agoraStarted()

Call this function to send a message indicating that Agora has started to the engine. This action will trigger the `agoraStarted` message.

```js
NagwaRenderingEngine.agoraStarted();
```

### updateChatStatus(status)

Use this function if you want to update the chat status and enable or disable it, By calling this function with `false`, you can disable the chat feature, and with `true`, you can enable it again.

```js
NagwaRenderingEngine.updateChatStatus(false); // will disable the chat
```

```js
NagwaRenderingEngine.updateChatStatus(true); // will enable the chat
```

### updateCurrentQuestionAskingStatus

Use This function if you want to update the current question status to be whether `Initial`, `In_Progress`, or `Time_Is_Up`

When `current_question_asking_status` is set to `In_Progress`, the student will be able to scroll and can submit the question answer once. However, when `current_question_asking_status` is set to `Time_Is_Up`, the student won't be able to scroll or submit the answer anymore, indicating that the time limit for the activity has expired. This function allows you to control the time-limited behavior of the application as required.

```js
NagwaRenderingEngine.updateCurrentQuestionAskingStatus('Initial');
```

```js
NagwaRenderingEngine.updateCurrentQuestionAskingStatus('In_Progress');
```

```js
NagwaRenderingEngine.updateCurrentQuestionAskingStatus('Time_Is_Up');
```

---

## Engine Events

The engine offers various events to listen to for custom actions and view updates. These events empower you to interact with the engine, respond to changes, update the view and enhance the user experience.

### engineLoaded

This event will be fired when the engine is fully loaded and ready for use. It serves as an indication that all necessary components have been initialized, and you can now start interacting with the engine and its functionalities.

```js
window.addEventListener('message', message => {
    const data = JSON.parse(message.data);
    if (data.messageKey === 'engineLoaded') {
        // do your action here
    }
});
```

### currentScreenUpdated

This event will be fired whenever the current screen receives new data from Firebase and is updated accordingly. This event serves as a notification that the screen content has changed, allowing you to synchronize your view with the latest data received from the Firebase.

```js
window.addEventListener('message', message => {
    const data = JSON.parse(message.data);
    if (data.messageKey === 'currentScreenUpdated') {
        console.log(data.screenID);
        // do your action here
    }
});
```

### interactionUpdated

This event will be fired when the current screen receives new interaction data from Firebase. Use this event to update your view and provide an interactive user experience.

```js
window.addEventListener('message', message => {
    const data = JSON.parse(message.data);
    if (data.messageKey === 'interactionUpdated') {
        console.log(
            data.interactions.original,
            data.interactions.formatedInteractions,
            data.currentScreen,
            data.questionID,
            data.questionType, // aggregated_all_possible_answers, aggregated_only_student_answers, separated
            data.choices, // if aggregated_all_possible_answers will contain all choices
            data.correctAnswers
        );
        // do your action here
    }
});
```

Example of the output object if the question type is `aggregated_all_possible_answers` or `aggregated_only_student_answers`:

```json
{
    "currentScreen": "4",
    "questionID": "245178050680.2",
    "questionType": "aggregated_all_possible_answers",
    "choices": ["أ", "ب", "ج", "د"],
    "totalInteractions": 1,
    "interactions": [
       {
            "count": 1,
            "percentage": 100,
            "answer": "أ"
        },
        {
            "count": 0,
            "percentage": 0,
            "answer": "ب"
        },
        {
            "count": 0,
            "percentage": 0,
            "answer": "ج"
        },
        {
            "count": 0,
            "percentage": 0,
            "answer": "د"
        }
    ],
    "correctAnswers": [], // always empty array (for now :D)
    "currentStudentAnswer: "أ", // or null if the student didn't answer
    "messageKey": "interactionUpdated"
}
```

Example of the output object if the question type is `separated`:

```json
{
    "currentScreen": "9",
    "questionID": "363128187320",
    "questionType": "separated",
    "choices": [], // seperated questions don't have choices
    "totalInteractions": 1,
    "interactions": [
        {
            "answer": "43242",
            "studentID": "111111111111",
            "studnetName": "the educator"
        }
    ],
    "correctAnswers": [], // always empty array (for now :D)
    "currentStudentAnswer: "43242", // or null if the student didn't answer
    "messageKey": "interactionUpdated"
}
```

### drawingToolsUpdated

This event is fired when the current screen receives new drawing tools data from Firebase.

```js
window.addEventListener('message', message => {
    const data = JSON.parse(message.data);
    if (data.messageKey === 'drawingToolsUpdated') {
        console.log(data.mode, data.color, data.stroke);
        // do your action here
    }
});
```

### questionAskingStatusUpdated

This event will be fired when the `questionAskingStatus` status is updated.

```js
window.addEventListener('message', message => {
    const data = JSON.parse(message.data);
    if (data.messageKey === 'questionAskingStatusUpdated') {
        console.log(data.questionAskingStatus);
        // values of questionAskingStatus is `Initial`, `In_Progress`, or `Time_Is_Up`
        // do your action here
    }
});
```

### agoraStarted

This event will be fired when the Agora starts.

```js
window.addEventListener('message', message => {
    const data = JSON.parse(message.data);
    if (data.messageKey === 'agoraStarted') {
        // do your action here
    }
});
```

### chatStatusUpdated

This event will be fired when the chat status is updated.

```js
window.addEventListener('message', message => {
    const data = JSON.parse(message.data);
    if (data.messageKey === 'chatStatusUpdated') {
        console.log(data.isChatEnabled);
        // do your action here
    }
});
```

### historyStatusUpdated

This event will be fired when the history status is updated.

-   `isUndoStackEmpty`: indicates whether the undo stack is empty or not.
-   `isRedoStackEmpty`: indicates whether the redo stack is empty or not.
-   `isScreenEmpty`: indicates whether the current screen is empty or not.

```js
window.addEventListener('message', message => {
    const data = JSON.parse(message.data);
    if (data.messageKey === 'historyStatusUpdated') {
        console.log(data.isUndoStackEmpty, data.isRedoStackEmpty, data.isScreenEmpty);
        // do your action here
    }
});
```
