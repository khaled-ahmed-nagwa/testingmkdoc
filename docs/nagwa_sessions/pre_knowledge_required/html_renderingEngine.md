# HTML Rendering Engine

To support the drawing/handling actions functionality while conducting the session, we depend on our customized “HTML Rendering Engine”. The rendering engine is responsible for displaying drawings, visualizations, activities, and questions within the application.


## Main Features

1. Drawing Tools: Educators have access to a range of drawing tools, including various colors and sizes for creating visuals.
2. Undo, Redo, and Reset: Educators can undo or redo actions while drawing or editing, and they can also reset the canvas to its original state.
3. Clear Screen: A simple option to clear the canvas and return to the default settings
4. Question Engine Support: The engine is capable of rendering and displaying questions for students to answer.
5. Activities Engine Support: Interactive activities can be rendered by the engine, allowing users to participate actively.
6. Firebase Data Syncing: The engine seamlessly syncs data with the Firebase platform, ensuring efficient data management.



### Main Technologies Used
The HTML rendering engine is built using:

   - React
   - Redux Toolkit
   - Firebase
   - Webpack
   - Babel.


## Engine Main Function

<table>
    <thead>
        <tr>
            <th style="width: 50%;">Main Events & Functions</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>NagwaRenderingEngine.updateScreen('SCREEN_ID')</code></td>
            <td>Call this function if you want to update the currently active screen and ensure that the changes are
                also updated in Firebase.</td>
        </tr>

        <tr>
            <td><code>NagwaRenderingEngine.changeTool({<br>color: 'red',<br>strokeWidth: 3,})</code></td>
            <td>Call this function to update the currently active tool or pen with a new color, size, or type and
                start using it inside the app view. The function takes an object as a parameter that may contain any
                of these three properties: color, strokeWidth, type. Type can contain [Draw, DeletePart, or Normal.]
            </td>
        </tr>

        <tr>
            <td><code>NagwaRenderingEngine.undo()</code></td>
            <td>This function allows you to perform an undo action for your last action and remove it within the
                application. By calling the undo() function, you can effortlessly revert the most recent action and
                continue undoing previous actions if necessary.</td>
        </tr>

        <tr>
            <td><code>NagwaRenderingEngine.redo()</code></td>
            <td>This function enables you to redo your last undo action and retrieve it. With the help of our redo
                stack, which tracks all your undo actions during the current session, you can perform multiple redo
                actions as needed. Restoring changes that were previously undone becomes effortless.</td>
        </tr>

        <tr>
            <td><code>NagwaRenderingEngine.clearScreen()</code></td>
            <td>Call the clearScreen() function to clear the entire current screen view. Important to note that
                executing this action will remove all content, including drawings and images, from the current
                screen.</td>
        </tr>

        <tr>
            <td><code>NagwaRenderingEngine.agoraStarted()</code></td>
            <td>Call this function to send a message to the engine indicating that Agora has started. This action
                will trigger the agoraStarted message.</td>
        </tr>

        <tr>
            <td><code>NagwaRenderingEngine.updateChatStatus(false||true);</code></td>
            <td>Use this function if you want to update the chat status and enable or disable it. By calling this
                function with false, you can disable the chat feature, and with true, you can enable it again.</td>
        </tr>

        <tr>
            <td>NagwaRenderingEngine.updateCurrentQuestionAskingStatus('value');</td>
            <td>Use this function if you want to update the current question status to be whether Initial,
                In_Progress, or Time_Is_Up.</td>
        </tr>
    </tbody>
</table>


## Engine Main Events


<table>
    <thead>
        <tr>
            <th style="width: 40%;">Engine Events</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>engineLoaded</code></td>
            <td>This event will be fired when the engine is fully loaded and ready for use. It serves as an indication that all necessary components have been initialized, and you can now start interacting with the engine and its functionalities.</td>
        </tr>
        
        <tr>
            <td><code>currentScreenUpdated</code></td>
            <td>This event will be fired whenever the current screen receives new data from Firebase and is updated accordingly. This event serves as a notification that the screen content has changed, allowing you to synchronize your view with the latest data received from Firebase.</td>
        </tr>
        
        <tr>
            <td><code>interactionUpdated</code></td>
            <td>This event will be fired when the current screen receives new interaction data from Firebase. Use this event to update your view and provide an interactive user experience.</td>
        </tr>
        
        <tr>
            <td><code>drawingToolsUpdated</code></td>
            <td>This event is fired when the current screen receives new drawing tools data from Firebase.</td>
        </tr>
        
        <tr>
            <td><code>questionAskingStatusUpdated</code></td>
            <td>This event will be fired when the questionAskingStatus status is updated.</td>
        </tr>
        
        <tr>
            <td><code>agoraStarted</code></td>
            <td>This event will be fired when the Agora starts.</td>
        </tr>
        
        <tr>
            <td><code>chatStatusUpdated</code></td>
            <td>This event will be fired when the chat status is updated.</td>
        </tr>
        
        <tr>
            <td><code>historyStatusUpdated</code></td>
            <td>This event will be fired when the history status is updated, used to handle empty undo/redo stacks.</td>
        </tr>
        
        <tr>
            <td><code>logMsg</code></td>
            <td>This event will be fired when the engine has new logs.</td>
        </tr>
    </tbody>
</table>


???+ info "Want to Learn More ! 🤩"
    If you're eager to explore more about the HTML rendering engine, please navigate to the next page, which contains comprehensive details about the engine, along with a comprehensive list of examples showcasing its events and functions.
