# Session Material Overview

Each session has it's own material , this material is a Zip file that contains the assets that the educator will use in the session, including slides, images, and questions, the zip folder includes 2 main components:

- **XML File**: This file contains the session data, which includes various slides. Each slide is identified by a number and categorized by its type. The types of slides can be either "image" slides or "question" slides. In the case of question slides, additional attributes are included, such as question_id, question_type, question_options, and key, which provide relevant information about the question.
- **Slides Folder**: Within this folder, there are sub-folders, and each sub-folder represents a single slide from the session. These slides can be either images or XML files that represent questions. 
!!! tip "You can check a sample content of the session material ZIP file from here [Package Samples](https://drive.google.com/drive/folders/1SqF4t9mb51dY4kNpVbybHaLfqKYbzJw2?usp=sharing) " 

Each session has its own unique material folder. Therefore, each time we start a new session, we must ensure that we download the specific session material.

??? note " Checking If Material Exist ?"
    The `checkIfMaterialExist` function checks the local device for the presence of a material using its file ID. This function determines whether the material is available locally and returns true or false accordingly.

## Linking Material File with a Session

The session material is uploaded and selected from the portal when creating the session, as the name of the material folder is the same as session-id, 

!!! warning "Once the session starts the educator cannot modify the content of the material anymore."

??? abstract "Downloading Material Screen" 
    <iframe frameborder="0" style="width:100%;height:452px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G11MQlx88TAYsxnEKOmk2ySIu_1NQBG3dY"></iframe>

??? abstract "Material  Folder Structure" 
    <iframe frameborder="0" style="width:100%;height:292px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1-Gw63LKD8NnLwsuyLnwxc2YjyCgktbIV"></iframe>
    <iframe frameborder="0" style="width:100%;height:750px;" src="https://viewer.diagrams.net/?tags=%7B%7D&highlight=0000ff&edit=_blank&layers=1&nav=1#G1s8OFgaXQS9sMU7b5ewvzN8hhScstm6XY"></iframe>