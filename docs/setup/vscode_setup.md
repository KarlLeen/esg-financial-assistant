# Recommended Visual Studio Code Setup for the ESG Financial Assistant Project

This document outlines the recommended setup for using Visual Studio Code (VS Code) to work on the ESG Financial Assistant project. Following these guidelines will help ensure a smooth development experience.

## 1. Install Visual Studio Code

If you haven't already, download and install Visual Studio Code from the [official website](https://code.visualstudio.com/).

## 2. Recommended Extensions

To enhance your development experience, consider installing the following extensions:

- **Python**: Provides rich support for the Python language, including IntelliSense, linting, and debugging.
- **Pylance**: A fast and feature-rich language server for Python, offering type checking and auto-completion.
- **Prettier - Code formatter**: Automatically formats your code to ensure consistency across the project.
- **ESLint**: Integrates ESLint into VS Code for JavaScript and TypeScript linting.
- **GitLens**: Enhances the built-in Git capabilities, providing insights into code authorship and history.
- **Jupyter**: Supports Jupyter notebooks, allowing you to run and edit notebooks directly within VS Code.

## 3. Recommended Settings

To optimize your VS Code environment for this project, consider adding the following settings to your `settings.json` file:

```json
{
    "python.pythonPath": "path/to/your/venv/bin/python",
    "editor.formatOnSave": true,
    "python.formatting.provider": "autopep8",
    "python.linting.enabled": true,
    "python.linting.pylintEnabled": true,
    "editor.tabSize": 4,
    "editor.insertSpaces": true
}
```

Make sure to replace `"path/to/your/venv/bin/python"` with the actual path to your Python virtual environment.

## 4. Setting Up the Workspace

1. **Open the Project**: Launch VS Code and open the `esg-financial-assistant` directory.
2. **Create a Virtual Environment**: Follow the instructions in `local_environment.md` to set up a Python virtual environment.
3. **Install Dependencies**: Use the terminal in VS Code to install the required packages from `requirements.txt`.

## 5. Additional Resources

- For more information on using VS Code, refer to the [official documentation](https://code.visualstudio.com/docs).
- Explore the extensions marketplace for additional tools that may enhance your workflow.

By following these guidelines, you will be well-equipped to contribute to the ESG Financial Assistant project effectively. Happy coding!