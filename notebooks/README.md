# Jupyter Notebooks

This directory contains Jupyter notebooks used for data analysis, exploration, and model development in the Youth ESG Financial Assistant project.

## Available Notebooks

- **data-cleaning.ipynb**: Processes and cleans the raw datasets, handling missing values and standardizing formats.

## Planned Notebooks

- **data-exploration.ipynb**: Exploratory data analysis to understand dataset characteristics and relationships.
- **feature-engineering.ipynb**: Creation of derived features and transformation of data for model input.
- **model-development.ipynb**: Development and training of recommendation algorithms.
- **model-evaluation.ipynb**: Evaluation and testing of model performance.
- **visualization.ipynb**: Visualizations of ESG and financial data for project presentations.

## Usage Guidelines

1. **Environment Setup**: Make sure you have activated the project's virtual environment before running these notebooks:
   ```bash
   source venv/bin/activate  # On macOS/Linux
   venv\Scripts\activate     # On Windows
   ```

2. **Notebook Server**: Start the Jupyter notebook server from the project root:
   ```bash
   jupyter notebook
   ```

3. **Dependencies**: All notebooks rely on packages listed in the project's `requirements.txt`. Ensure these are installed.

4. **Data Access**: The notebooks expect data files to be in the `/data` directory. Make sure all required datasets are available.

5. **Execution Order**: For proper workflow, execute the notebooks in the following order:
   - data-cleaning
   - data-exploration
   - feature-engineering
   - model-development
   - model-evaluation

## Contributing

When creating new notebooks or modifying existing ones, please follow these guidelines:

1. **Documentation**: Include markdown cells explaining the purpose and methodology of each analysis step.

2. **Code Organization**: Keep code organized in logical sections with clear cell divisions.

3. **Output Management**: Clear outputs before committing to reduce repository size and merge conflicts.

4. **Naming Convention**: Use descriptive names for notebooks, following the pattern `<purpose>-<description>.ipynb`.

5. **Resource Management**: Close connections and free resources at the end of notebooks.

For more details on coding standards, refer to the [Coding Standards](../docs/development/coding_standards.md) documentation.
