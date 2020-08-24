# nbgrader toolbox

[nbgrader](https://github.com/jupyter/nbgrader) is an open-source software systen for assigning and grading Jupyter notebooks. 
nbgrader has a rich working environment and is operable through either commandline or
a GUI Jupyter extension called Formgrader. [nbgrader's official documentation](https://nbgrader.readthedocs.io/en/stable/)
provides a overview of the application and how to use it in its vanilla form.

The nbgrader_toolbox provides a couple fo Python scripts with some linked excutable *.bat* files,
through which we can easily manipulate the nbgrader ecosystem.

These custom tools are attempting to simplify the workflow with nbgrader from installation
to daily usage and to provide some tools to implement nbgrader into the courses tought at the University of Oulu.
There are a lot of differences between the differences courses and how their system
of assignments is structured, and so the tools will need to be continuosly updated and
and their funcitonality expanded while they are being tested on various other courses.

Current version of the nbgrader_toolbox is working with the infrastructure of the
Machine Vision course. 



## Requirements 
1. [Conda](https://www.anaconda.com/) is installed on your computer.
2. Python 3.x is used through conda
3. Python is added to the system PATH
4. **Create a virtual environment called *nbgrader_env***. This step is crucial(!) in order to have
all the tools working properly. You can create a new environment or clone existing one, so you don't have
reinstall a lot of the basic packages. For more on how to manage virtual
environments, checkout the [conda documentation](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html)
It is currently done in this manner due to the development purposes
and it wouldn't be good to try and polute the *base* environment with developmental progress. In the
future builds, this mandatory step will be removed and the user will simply choose, which environment
they wish to install the application into. 

## Installation
Upon installing conda and creating **nbgrader_env**, proceed as follows:

1. Clone this repository or download it as a zip file and extract the downloaded archive.
2. Double-click the executable `install_nbgrader.bat`

Done!
<br />
<br />
Upon installation, the following hierarchy will get created:
- install_nbgrader.bat
- nbgrader (folder)
	- create_course_folder.bat
	- tools <br /> <br />
		*(.bat files)*
		- add_or_update_students.bat
		- autograde_assignment.bat	
		- launch_jupyter.bat
		- pull_assignments.bat
		- release_assignment.bat
		- sort_moodle_submissions.bat
		- update_grades_file.bat

		*(.py files)*
		- add_or_update_students.py
		- create_custom_config.py
		- get_grades_to_excel.py
		- git_assignments.py
		- late.py		
		- moodle_submission_sort.py
		- old_nbgrader_config.py
		- print_assignments.py				
		- release_assignment.py
		- send_feedback_to_students.py				
		- upload_grades.py

## Create course folder
1. Within the nbgrader folder, doublie-click the `create_course_folder.bat` file. 
2. A commandline window will appear. 
3. Select a name for the course. It doesn't matter what the names is.
4. You will be asked if you want to download the assignments from our private repository. 
Choose *y*. Course ID will be required.

The created course root folder can be stored wherever on the computer, however the file hierarchy within the course root folder
needs to remain unchannged and is to be followed. <br /> <br />
**Source** folder
> Containg the master versions of the assignments. The master versions are created according to the [official documentation](https://nbgrader.readthedocs.io/en/stable/user_guide/creating_and_grading_assignments.html)

**Release** folder
> Containing all the assignments, that have been released (= the student versions of the assignments.)

**Submitted** folder
> Contains all the submissions by the students. 


These folders have to follow a strict hierarchy established by the *nbgrader* original application. 
More information about the hierarchy [here](https://nbgrader.readthedocs.io/en/stable/user_guide/philosophy.html)

Everything within the nbgrader course is stored in the **gradebook.db** database file. This file contains all the information
about the students, their grades, the assignments and so on. <br />
WARNING! This file might not be created immediately, when you create the course folder, however it will get generated after we do our first necessary operations.

## Step-by-step operating guide

### Synchronize the students
> We need to synchronize the students, that are enrolled in our Moodle with the student list stored within the **gradebook.db** file.
1. Go to the Moodle course page.
2. Change the Moodle interface language to English. IMPORTANT. It won't work otherwise. 
3. Click **Participants** in the right vertical menu.
4. Select all the participants, however exclude the teachers and leave only students selected.
5. In the roll-down menu below the participants list, select **Download table data as** *comma seperated values .csv*
6. Locate the downloaded .csv file and move/copy it into the course root folder, that we created earlier.
7. Within the course folder, double-click the **add_or_update_students.bat**. 
8. Write or copy/paste the name of the downloaded .csv file.
<br />
You should all the students that have been added listed in the command-line. 

**Check the course and the students**
> When done importing the students, let's check the course through the nbgrader Formgrader extension for Jupyter.

1. Within the course folder, double-click **launch_jupyter.bat**.
2. In Jupyter, click the **Formgrader**, the last item in the top horizontal menu.
3. In Formgrader, we can now see the available assignments, that are stored in the *source* folder. These assignments are not stored in the *gradebook.db* file yet,
they are simply listed as detected assignments. 
4. In the vertical menu on the left side, select **Manage students**. 
5. We should now see a complete list of the students corresponding to the one in Moodle.


### Release an assignment
> We want to generate the student version of the master assignment. Meaning, we want to remove all the tests, solutions and leave blank spaces for the students to fill in. 

1. In the course folder, double-click **release_assignment.bat**. It will list all the available assignments in a table on top.
2. Write, which assignments you wish to release. You have to write the full name of the assignment.
3. Provide the due date within the format that is specified. *YYYY-MM-DD HH:MM:SS*. Make sure the due date is the same as in the Moodle page for the assignment.
4. The released assignment is stored in the *release* folder. 
5. Archive the released files and upload them to Moodle.

### Sort Moodle submissions
!! We are collecting only the *.ipynb* files.
> After the deadline, let's collect the submissions as follows:

1. Within the moodle course page, set the interface language to English in the top roll-down menu.
2. Go to the assignment page.
3. Select all the submissions and select **Download selected submissions**.
4. Locate the downloaded archive and move into the **submitted** subfolder. **coursef_root_folder/submitted**.
5. Copy the name of the downloaded archive. Don't change the name!
6. In the course root folder, double-click the **sort_moodle_submissions.bat**.
7. Paste the name of the submission archive and hit Enter. 
8. We should have the archive now extracted according to the hierarchical rules. 
9. Delete the archive file.

> In Jupyter (launch_jupyter.bat if closed), we can now see that for the assignment, a number of submissions have been added. 
