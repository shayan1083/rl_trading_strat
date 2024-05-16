Create VENV:
1) Enter terminal
2) navigate to main folder
3) python3 -m venv {venv name}

Activate env:
1) Enter terminal
2) navigate to main folder
3) type "source {venv name}/bin/activate"

- the name of the virtual environment should be next to the terminal prompt if it is activated
- everything installed when the venv is running will be installed locally

Install Libraries:
1) Enter terminal
2) pip3 install -r requirements.txt

- strat.ipynb has the code
- When in "strat.ipynb", select kernel in the top right, and choose {venv name} to enter virtual environment
- "deactivate" in terminal deactivates virtual env