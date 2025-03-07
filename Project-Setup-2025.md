# 1. Project Setup
To organize your work on **PACE**, create a main `~/clef` folder. This will be your working directory for cloning repositories and managing project files.

1. Navigate to your home directory: `cd ~`
2. Create the `clef` directory: `mkdir clef`

Next, we will authenticate to GitHub using the GitHub CLI `gh` so we can clone repos.


# 2. Downloading the GitHub CLI `gh`
To authenticate to GitHub, first we will download and install the GitHub CLI `gh` 
directly using `curl` and add it to PATH, follow these steps:

1. Create a `bin` directory in your home folder:
    ```
    mkdir -p ~/bin
    ```
2. Get exact download URL via GitHub API:
    ```
    LATEST_URL=$(curl -s https://api.github.com/repos/cli/cli/releases/latest | grep "browser_download_url.*linux_amd64.tar.gz" | cut -d '"' -f 4)
    ```
2. Download the `gh` binary file into the `~/bin` directory using curl:
    ```
    curl -L "$LATEST_URL" -o ~/bin/gh.tar.gz
    ```
3. Extract the file using `tar`:
    ```
    tar -xzf ~/bin/gh.tar.gz -C ~/bin --strip-components=2 gh_*/bin/gh
    ```
4. Remove the downloaded `tar.gz` file:
    ```
    rm ~/bin/gh.tar.gz
    ```
5. Add the `~/bin` directory to your PATH by editing your shell configuration file. Add the following line at the end of the file:
    ```
    export PATH="$HOME/bin:$PATH"
    ```
6. Apply the changes to your current session:
    ```
    source ~/.bashrc
    ```
Now you should be albe to run `gh` from any directory. To verify the installation, run: 
```
gh --version
```

# 3. Authenticating to GitHub using GitHub CLI
This section streamlines the authentication process to GitHub using the 
GitHub CLI `gh`, which simplifies the SSH setup. 

### Step 1: Authenticate to GitHub using GitHub CLI
1. Run `gh auth login` to begin the authentication process.
2. When prompted, select **SSH** as the preferred protocol for Git operations.
3. If you don't already have an SSH key, `gh` will prompt you to generate one. Follow the on-screen instructions to create a new SSH key.
4. `gh` will automatically add your SSH key to your GitHub account. Follow any additional prompts to complete the process.
5. After completing the setup, run `gh auth status` to check if you're successfully authenticated.

### Step 2: Verify GitHub User Information (Optional)
It's good practice to ensure your Git identity is correctly set:
1. **Check Git Configurations:** Run `git config --list` to see your Git configurations, including user name and email.
2. **Set Git User Information If Not Set:** If not already set, configure your Git user information:
```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```
Replace with your GitHub email and name.


# 4. Use the `clef-project-template` to create your repo
The [**`clef-project-template`**](https://github.com/dsgt-kaggle-clef/plantclef-2025/tree/main) is a template repo for all CLEF projects. It's meant to be forked and used as a starting point for new projects.

1. Head over to the repo [dsgt-kaggle-clef/clef-project-template](https://github.com/dsgt-kaggle-clef/plantclef-2025/tree/main)
2. Click on the button "**Use this template**" in the upper rigth corner.
3. Give a name to the repo. The name should be: **`taskname-YYYY`**. For example, the PlantCLEF repo will be `plantclef-2025`.
4. Change the view access from **"Private"** to **"Public"**.
5. Click on **"Create repository"**


# 5. Cloning the Repository
This step in the project setup process involves cloning the newly created repository to the `~/clef` directory on PACE. In this example, we'll use the [**`plantclef-2025`**](https://github.com/dsgt-kaggle-clef/plantclef-2025/tree/main) repository. 

**Note:** You should use your newly created repo instead of `plantclef-2025`!

### Step 1: Clone the Repository
1. **Navigate to Desired Directory:** Choose the directory where you want to clone the repository. For instance, `cd ~/clef`.
2. **Clone the Repository:** Run the following command to clone the `plantclef-2025` repository:
    ```
    git clone git@github.com:dsgt-kaggle-clef/plantclef-2025.git
    ```
3. **Navigate into the Repository Directory:** After cloning, move into the repository's directory:
    ```
    cd plantclef-2025
    ```

### Step 2: Verify the Setup
1. **Check Repository Content:** Verify that the repository content is correctly cloned by listing the files with `ls`.
2. **Check Branch Status:** Use `git status` to ensure you're on the correct branch and to see if there are any changes.

### Step 3: Follow the TODOs in the `clef-project-template`
Follow the TODOs section in the README.md file. 

**Note:** Don't create the virtual environment yet. This will be done in the next step.

1. Update the `my_task_package` directory with the name of your task package e.g. `birdclef`, `plantclef` or `longeval`.
2. Update the `pyproject.toml` file with the following elements:
    1. `project:name` should be a hyphenated version of the task package
    2. `project:authors` should be updated with the names of the team members
    3. `project:urls` should be updated with the corresponding URLs for the project
    4. `tools.setuptools.packages.find:include` should be updated with the directory name of the task package
3. Update `user/my-username` and the corresponding README.md file with the username and a description of the user's directory.

If you're unsure about the steps above, refer to the [`plantclef-2025`](https://github.com/dsgt-kaggle-clef/plantclef-2025/tree/main) repo for reference.

We're almost done. Next, create a Virtual Environment to isolate project's dependencies.


# 6. Setting Up a Virtual Environment
To keep dependencies isolated, we will create a virtual environment in your `~/scratch` directory and install the required packages.

After finishing the TODOs from the `clef-project-template`, do the following: 
<!-- 1. Navigate to the scratch directory: `cd ~/scratch`
2. Create the Virtual Environment: `python -m venv .venv`
3. Activate the Virtual Environment: `source .venv/bin/activate`
4. Navigate to your repo: `cd ~/clef/plantclef-2025`
5. Intall the package in editable mode: `pip install -e .`
6. Install dependencies: `pip install -r requirements.txt`
7. Verify the installation: `pip list`
8. Run the package tests using the `pytest` command: `pytest -v tests/`
9. Add the **pre-commit hooks** to your repo. This ensures that the code is formatted correctly and that the tests pass before committing: `pre-commit install` -->

1. Navigate to the scratch directory:
    ```
    cd ~/scratch
    ```
2. Create the Virtual Environment:
    ```
    python -m venv .venv
    ```
3. Activate the Virtual Environment: 
    ```
    source .venv/bin/activate
    ```
4. Navigate to your repo:
    ```
    cd ~/clef/plantclef-2025
    ```
5. Intall the package in editable mode:
    ```
    pip install -e .
    ```
6. Install dependencies:
    ```
    pip install -r requirements.txt
    ```
7. Verify the installation:
    ```
    pip list
    ```
8. Run the package tests using the `pytest` command:
    ```
    pytest -v tests/
    ```
9. Add the **pre-commit hooks** to your repo. This ensures that the code is formatted correctly and that the tests pass before committing:
    ```
    pre-commit install
    ```

Your environment is now set up and ready for development.


# 7. Using `branches` for Development
Creating a new branch ensures that your development work is separated from the main branch, allowing for easier code management and review.

1. **Fetch All Branches (Optional):** If you want to see all existing branches first, run: 
    ```
    git fetch --all
    ```
2. **Create a New Branch:** Create a new branch off the main branch for your development work:
    ```
    git checkout -b username/your-branch-name
    ```
    Replace `your-branch-name` with a meaningful name for your development work, typically like `username/data-analysis`, or similar prefixes.
3. **Verify New Branch:** Ensure you're on the new branch with `git branch`. The new branch should be highlighted.

### Step 1: Naming Convention for Jupyter Notebooks
When creating new Jupyter notebooks, adhere to the following naming convention:

- **Format:** `initials-date-version-title.ipynb`
- **Explanation:**
    - **initials:** Your initials (e.g., Tony Stark → ts).
    - **date:** The date you created the notebook in YYYYMMDD format.
    - **version:** A two-digit version number, starting from `00`.
    - **title:** A brief, hyphen-separated title describing the notebook's purpose.

**Example**
If Tony Stark creates a data analysis notebook on January 18, 2025, 
the filename would be:
- `ts-20250118-00-data-analysis.ipynb`

### Step 2: Regularly Commit Changes
Remember to regularly commit your changes to maintain a record of 
your work and to synchronize with the remote repository.

1. **Stage Changes:** Use `git add .` to stage all changes in the 'notebooks' directory.
2. **Commit Changes:** Commit with a descriptive message:
    ```
    git commit -m "Add initial data analysis notebook by TS"
    ```
3. **Push to Remote:** Push your changes to the remote repository:
    ```
    git push -u origin username/your-branch-name
    ```

That's it! You're now all set to start developing on your project. Happy coding! 😊💻
