# Getting started with MINERVAS Online System

Since the MINERVAS is deployed on [Coohom](https://www.coohom.com/) ([Kujiale](https://www.kujiale.com) is the Chinese brand of Coohom), a web-based 3D design platform, user might need to register and login to MINERVAS online system for further usage. 

> **TODO**: TO BE UPDATE AFTER MINERVAS ACCOUNT UPDATED

## Account Related Usage
Click [here](https://share.hsforms.com/1JqF4gRE2Ri2z7ul1eY5rMw4irvw?kpm=qkWL.9b0955304addf074.a289e9d.1629387341506) to apply for an free trial account.

<!-- 1. Visit [https://www.kujiale.com/coohomcloud/minervas#/scene](https://www.kujiale.com/coohomcloud/minervas#/scene)
2. Login Account： Same as the Kujiale account, if it is a trial account, it will be allocated by the business separately
3. Login Password： Same as the Kujiale account password, if it is a trial account, it will be notified by the business separately

> Tips： It is recommended to use Google Chrome to log in -->

<!-- ### Account login

 Click the account login on the system page, enter the account and password, and click login to log in to the home page of the EUS system.

![User Login](images/user_login.png) -->

<!-- ### Change Password

To change the password, you need to enter the Kujiale homepage（https://www.kujiale.com/）, And then click the person’s avatar in the upper right corner of the system page, click Account Settings in the personal information pop-up window, click Account Security in the account settings page, and then click [Modify Password] in the Security Information Module. In the Modify Password pop-up window, enter the original password And the new password, the new password format requirements: ①The length is 8-16 characters; ②Cannot use spaces; ③Contain at least two combinations of numbers/letters/characters; ④Cannot contain illegal characters.。

![User Center](images/user_center.png)
![Security Information](images/security_information.png)
![Password Change](images/password_change.png) -->

## Create simulation task

After successful login, you will enter the EUS homepage-Scene Management.

## System Related Usage

After successfully login, you will enter the MINERVAS online system. Click *New Simulation Task* will create a new task. 

![Manage Scene](images/task_entry.png)

### Step-1
<span style="color:red">*TODO:* 图片需要更新成新版本的</span>

The first step to set the simulation task

1. click here to input task name.
2. The default setting is No, at this time, click Next to enter the visual configuration interface
3. Choose Yes to enter the DSL file configuration mode, you can complete the task configuration through the DSL file
4. click here to enter the next step

![Manage Scene](images/task_set.png)

#### DSL Usage

<span style="color:red">*TODO:* 内容待优化</span>

If you choose to create a simulation task with DSL file and enter the simulation task setting pop-up window.

1. The name of the task is required, which can record the main purpose of the task and facilitate the subsequent search for the task
2. The default number of repetitions is 1, and it is recommended to use it with random ability
3. After the merge download is turned on, the task results will be merged and processed, and all task results can be downloaded with one click (it is not recommended to open for a large number of scene tasks, too large task results will cause synthesis failure or download abnormality)
4. The task's processing of the scene is based on the DSL file, and the DSL file is currently in python format
5. The rendering results support selective output, rasterization refers to auxiliary images (depth maps, semantic maps, etc.), rendering as RGB images, and structure refers to extracting scene or camera information to an output json file
6. After completing the configuration, click OK to create a task, and automatically jump to task management.

![Create Task](images/create_task.png)
![DSL Upload](images/dsl_upload.png)

The essence of DSL writing is that the user customizes one or more subclasses in the python file. The subclasses: three subclasses inherited from the Processor class inside Ks-SDK, borrowing the interface provided by the SDK and inherited attributes, in the process() function Realize custom functions in, such as:

For details about DSL, please refer to [DSL Description Document](https://coohom.github.io/cloud-docs/)


### Step-2 

This step is used to filter the scene with both Query DSL or simple condition selections. The usage can be shown in the figure bellow:

![Manage Scene](images/scene_filter.png)

<span style="color:red">*TODO:* 是否需要说明目前场景数量受限制？</span>

1. Use the Query DSL or condition selections to filter interested scenes. 
2. Click on each scene based on the top-view visualization for further selection
3. Click on the top-view cover image to view the scene details
4. Click *Next* to go to the next step

### Step-3

> This section is used for user that do not use DSL in Step-1. For DSL user, check the *Task Management* section for your task.


#### Shooting & Track  

1. click here to choose track type，such as random track here
2. click here to set the  random track parameter 
3. click here to choose manually generate trajectories mode
4. click here to enter track editing mode
5. click here to set the  custom track parameter
   

![Manage Scene](images/track1.png)
![Manage Scene](images/track2.png)

# Task management

## Simulation Task

This module displays the status of simulation tasks, and provides task query, screening, and result download.

### Task List

1. Support filtering tasks in different states

2. You can search for the corresponding task by task id or task name

3. When the remaining available renderers are displayed

4. For task details, click to view the status of subtasks

5. Tasks whose task status is successful, support click to download task results

6. After the task is successful, the result data will be stored in the cloud for 14 days and needs to be downloaded in time

![Render Task](images/render_task.png)

### Subtask list

The subtask list can display the details of each subtask. Currently, one scene corresponds to one subtask;

1. Subtasks also support filtering subtasks by status

2. Subtasks support filtering subtasks by subtask id or scene id

3. The upper right corner of the subtask will display the specific time consumed by the subtask

4. Successful subtasks will show download links

Glossary:

Rendering task: Based on the scene and camera, use the photo-realistic renderer to generate RGB images

Auxiliary image tasks: based on the scene and camera, generate depth maps, semantic maps, instance maps, normal maps, etc.

Structural task: extract scene or camera information to an output json file

![Subtask List](images/subtask_list.png)

## Output task

This task is only open to users who have activated RW products. Users who have not purchased RW can ignore this part of the product introduction.

### Output task list

1. Support to filter tasks by status

2. Support filtering tasks by task id or scene id

3. The task status will be displayed in the upper left corner of the task. On average, each export task takes 15~20min. If the status is displayed as successful, you can view it normally in RW and use the corresponding scene for robot simulation training tasks.   

![Output Task](images/output_task.png)

<br/>

> NOTE: if you have any usage issue about MINERVAS system, please contact <minervas@qunhemail.com>.

