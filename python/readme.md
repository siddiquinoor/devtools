# Start a New Python Project: Step–by–Step
## Create/Go to your project folder

    cd /path/to/your/project-folder

If you haven’t created it yet:

    mkdir my_python_project
    cd my_python_project

## Create a Virtual Environment (Very Important)
This keeps your project dependencies clean and separate.
Run:

    /usr/local/bin/python3 -m venv venv

This will create a folder named venv/ inside your project.

## Activate the Virtual Environment
macOS / Linux:

    source venv/bin/activate

After activation, you'll see:

    (venv) $

Now anything you install goes only to this project.

## Install Packages Using Local pip3
Since you're inside the venv, just run:
    
    pip install <package-name>

But if you want to explicitly use your installed pip:

    /usr/local/bin/pip3 install <package-name>


## Create Your Main Python File

    touch main.py

Edit it (VS Code recommended):

    code main.py

Example code:
    
    print("Hello, Python project!")

Run:

    python main.py


## Freeze Dependencies (optional but recommended)

    pip freeze > requirements.txt

When deploying or sharing, others can install:

    pip install -r requirements.txt


## Your Python project is now successfully set up!
You can also create a best-practice project structure like:

    my_python_project/
    │── venv/
    │── src/
    │   └── main.py
    │── tests/
    │── requirements.txt
    │── README.md

