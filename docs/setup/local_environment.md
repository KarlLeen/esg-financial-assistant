# Local Environment Setup Guide

## Setting Up a Local Python Environment

To work on the Youth ESG Financial Assistant project locally, follow these steps to set up your Python environment.

### 1. Install Python

Ensure you have Python 3.7 or higher installed on your machine. You can download it from the official [Python website](https://www.python.org/downloads/).

### 2. Create a Virtual Environment

Creating a virtual environment helps manage dependencies for the project without affecting your global Python installation.

Open your terminal and navigate to the project directory:

```bash
cd path/to/esg-financial-assistant
```

Then, create a virtual environment:

```bash
python -m venv venv
```

### 3. Activate the Virtual Environment

- **On macOS and Linux:**

```bash
source venv/bin/activate
```

- **On Windows:**

```bash
venv\Scripts\activate
```

You should see the virtual environment name (e.g., `(venv)`) in your terminal prompt, indicating that it is active.

### 4. Install Dependencies

With the virtual environment activated, install the required dependencies listed in `requirements.txt`:

```bash
pip install -r requirements.txt
```

### 5. Verify Installation

To verify that the dependencies are installed correctly, you can run:

```bash
pip list
```

This command will display a list of installed packages. Ensure that the necessary packages for the project are included.

### 6. Deactivate the Virtual Environment

When you are done working on the project, you can deactivate the virtual environment by running:

```bash
deactivate
```

This will return you to your system's default Python environment.

### Additional Notes

- Make sure to activate the virtual environment each time you start working on the project.
- If you encounter any issues during installation, refer to the troubleshooting section in the project's documentation or seek help from the team.