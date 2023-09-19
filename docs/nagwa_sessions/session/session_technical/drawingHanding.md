# Handling Drawing 
The educator has the option to draw on the screen, and all drawings will be shared with the students in real-time.

!!! warning "Currently, the ability to draw is limited to the use of an Apple Pencil.and no other method is available."

## Initialize Drawing 
The `init` function is located inside ‘DrawingCubit’, it’s called when the user joins a session, Its required parameters are session id, file id, user id, and the user name, The `init` function in the WebView initializes the rendering engine to establish a connection with the session Firestore and retrieve all the necessary data.
```dart title="Initialize Drawing"
window.NagwaRenderingEngine.init({
    name: 'Mohamed Ahmed Mahmoud',
    role: 'educator', 
    rootElementID: 'root', // if not passed it will be `root`
    userID: '$currentUserId',
    sessionID: '$currentSessionId',
    packageBasePath: '', // the base path of the package to download the package
    enginesBasePath: '', // the base path of the engines
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


## Drawing Types
<table style="border-collapse: collapse; width: 100%; margin: 0 auto;">
    <tr>
        <th style="text-align: left; padding: 10px;">Pen Mode</th>
        <th style="text-align: left; padding: 10px;">Description</th>
    </tr>
    <tr>
        <td style="text-align: left; padding: 10px;">draw</td>
        <td style="text-align: left; padding: 10px;">For the draw pen type.</td>
    </tr>
    <tr>
        <td style="text-align: left; padding: 10px;">deletePart</td>
        <td style="text-align: left; padding: 10px;">For the erase object pen type used to delete entire paths or objects.</td>
    </tr>
    <tr>
        <td style="text-align: left; padding: 10px;">normal</td>
        <td style="text-align: left; padding: 10px;">For the normal pen mode, you can have your default cursor and perform regular actions like clicking to solve a question.</td>
    </tr>
</table>

## Change Pen Color 

Educators can draw using various types and colors of pens. Here’s a list of the available pens: 

- black("#4d4d4f")
- blue("#56a5e1")
- red("#e24c3c")
- green("#119f25")
- orange("#f4a304")
- purple("#ff2aff")

!!! note "To facilitate the erasing of points, we have a pen eraser with the color white eraser("#ffffff")." 
## Pen Stroke 
The "Stroke" refers to how thick the drawing pen's lines are. It's a number between 1 and 5, where 1 is thin and 5 is thick. When an educator picks a stroke size, it turns green to show that it's selected.

??? example "Drawing Pen Stroke"
    <iframe frameborder="0" style="width:100%;height:542px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1v7GcCpGt23VfEBx7Ky3HZbVlQ2yjzoJv"></iframe>

### Changing Between Pens Colors / Stroke
We are using the ‘changeTool’ function,  to send an update to the engine to change smoothly between pens, inside the function we run this js command
`"NagwaRenderingEngine.changeTool({ type: '${drawingType}' ${color} ${stroke} });"`

!!! info "`changeTool` function is located at the [lib/features/sessions/presentation/logic/drawing/drawing_cubit.dart](https://dev.azure.com/nagwa-limited/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/features/sessions/presentation/logic/drawing/drawing_cubit.dart&version=GBdevelopment) path."

??? example "Available Drawing Pen Types"
    <iframe frameborder="0" style="width:100%;height:532px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1UhTLb1fkXLBs3ETIN3mAWtx7tM1aizzE"></iframe>
------------------------------------------------
## Erasing Objects (Object Eraser)

To help educators delete specific objects or paths on the screen, they can use the "Object Eraser" tool.

To use the object eraser:
1. The Educator can select the erasing pen at the top of the screen.
2. Tap the switch button to turn on the object eraser.

!!! success "When it's on, the drawing type will change to ‘deletePart’ type, which is the mode for deleting objects"

???+ example "Object Eraser Screenshot"
    <iframe frameborder="0" style="width:100%;height:512px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1CwbIYs1ACjlnfmJX9q9IA3HJQ8HrbcFW"></iframe>

!!! question "What distinguishes the eraser pen, object eraser, and reset button?"
    All three options serve the purpose of deleting drawings on the screen, but they operate differently:

    - Pen Eraser: This tool functions as a white pen, which essentially covers the content on the screen with white color, making it invisible.
    - Object Eraser: The object eraser deletes entire objects or connected paths when you click on any point of the object.
    - Reset Button: Clicking this button resets the entire screen, removing all drawings and restoring it to its default state.


----------

## Drawing Tools Message Handler



The `drawingToolsUpdated` event is fired  from the HTML engine when the current screen receives new drawing tools data from Firebase. for that we are using the `drawingToolsMessageHandler` function which will be fired when we receive a drawingToolsUpdated event from the WebView, The message will contain the current drawing mode , the current pen color, and the current stroke, It checks the drawing mode to see whether it's `normal` , `draw` or `deletePart`

  1. It takes the arguments recived with event, decodes them as strings, and converts it to a map of strings and dynamic
  2. Then it gets the penColorHex, mode, and stroke values from the map and checks if it are equal to the selectedPen, currentDrawingType, and currentStroke values or not
  3. If it is not equal, it changes the selectedPen, currentDrawingType, and currentStroke values to the gotten values and emits the drawingrefresh


!!! info "The `drawingToolsMessageHandler` is located at the [lib/features/sessions/presentation/logic/drawing/drawing_cubit.dart](https://dev.azure.com/nagwa-limited/_git/Nagwa%20Sessions%20For%20Educators?path=/lib/features/sessions/presentation/logic/drawing/drawing_cubit.dart&version=GBdevelopment) path."

## Undo & Redo Drawing

The educator has the option to undo or redo a drawing action; these two buttons become active when the drawing stack got filled 

We handles this by calling the undo or redo functions in the html rendering engine `NagwaRenderingEngine.undo();`

<table style="border-collapse: collapse; width: 100%; margin: 0 auto;">
    <tr>
        <th style="text-align: left; padding: 10px;">Function</th>
        <th style="text-align: left; padding: 10px;">Description</th>
    </tr>
    <tr>
        <td style="text-align: left; padding: 10px;">Undo</td>
        <td style="text-align: left; padding: 10px;">The undo function allows you to perform an undo action for your last action and remove it. Within the application, we maintain an undo stack that keeps track of all user actions during the current session, enabling you to perform multiple undo actions as needed. By calling the undo() function, you can effortlessly revert the most recent action and continue undoing previous actions if necessary.</td>
    </tr>
    <tr>
        <td style="text-align: left; padding: 10px;">Redo</td>
        <td style="text-align: left; padding: 10px;">The redo function enables you to redo your last undo action and retrieve it. With the help of our redo stack, which tracks all your undo actions during the current session, you can perform multiple redo actions as needed. Restoring changes that were previously undone becomes effortless.</td>
    </tr>
</table>


??? example "Undo & Redo Screen"
    <iframe frameborder="0" style="width:100%;height:406px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1WSqPUwhuDJ0y8FSTs1yIvR59smuWjAIC"></iframe>

------------------

### Handling the Empty Status of Redo and Undo Stack 
In addition to the `undo()` and `redo()` functions, The engine fires a message to notify you when the undo or redo stack becomes empty. These messages trigger the `historyStatusUpdated` event, allowing you to update your view accordingly.

In our case, we make the two buttons inactive when this situation occurs, so educators cannot click on them anymore.

??? example "Inactive Undo & Redo Buttons"
    <iframe frameborder="0" style="width:100%;height:183px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1ajYAo4lUd5AtRyksVLb2oC4sN-4xKmbC"></iframe>

### History Status Updated Msg Handler

The `historyStatusUpdatedMsgHandler` function takes the args as a parameter, its main purpose is to check if the undo and redo stacks are empty or not and changes the isUndoStackEmpty and isRedoStackEmpty values

1. First, it decodes the arguments as strings and converts it to a map of strings and dynamic 

2. Then it gets the isUndoStackEmpty and isRedoStackEmpty values from the map and checks if they are equal to the isUndoStackEmpty and isRedoStackEmpty values or not.

3. If it is not equal, it changes the isUndoStackEmpty and isRedoStackEmpty values to the obtained values and emits the DrawingUndoRedoChanged.

------------------
 
## Reset Entire Screen

To clear the entire current screen view, simply call the clearScreen() function. Where we can run the js command `NagwaRenderingEngine.clearScreen();`

!!! warning "Executing reset action will remove all content, including drawings and images, from the current screen. Keep in mind that this action is reversible. You can use the undo button to return to the previous state, the data will be saved inside Firebase, preserving the previous state of your work."

