## What happens without Virtual_Environment ? ## 
- In real world projects are built with different language , packages , frame works and different type of versions.
- For that we need to install suitable performance versions and packages 
- If you install those directly in systems or IDE's that may cause unwanted results for other projects due to different versions.
- To avoid those conflicts we use Virtual Environments for each projects 

## How its works ##
- We can set vitual environment for each project in its own directory.
- After setting up we can install suitable pip packages , style guids modules etc..
- So that we can run our different projects with out any conflicts 

## How to setup ? ##
- For example if you are using python.
 - **Python -m venv venv** (This command inititalizes virtual environment to your folder)
 - **source venv/bin/activate** (This command used to activate ve)
 - Then install packages like pip install matplotlib etc..
 - **pip freeze > requirements.txt** (This cmd is used save all requirements for your project in a txt file) 
 - **deactivate** (After done your work you can deactivate the environments) 
 - Note : always remember when you open a project you should activate the virtual environmement again with the help of activate command.