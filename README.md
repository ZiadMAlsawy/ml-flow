# ML-Flow

During the setup of our ML CI workflow, we encountered several key issues and addressed them sequentially:

1. **Indentation Issues**  
   YAML is sensitive to spaces, so incorrect indentation caused the workflow to fail initially. Once fixed, the workflow structure became valid.

2. **Linter Step Missing a Run Command**  
   The `Linter Check` step initially had no `run:` command, so it was commented out.

3. **Missing Checkout Step**  
   The GitHub Actions runner starts with a **fresh virtual machine**, which does **not contain your repository files**.  
   - Without a checkout step, `pip install -r requirements.txt` failed because the file wasn’t present.  
   - After adding the checkout step, the runner could see `requirements.txt`, and pip succeeded.

4. **Pipeline Trigger**  
   The workflow was configured to trigger on **every push for all branches except `main`**, ensuring continuous integration checks run for development branches.

5. **Artifact Upload**  
   A step was added to upload the project's `README.md` as a **GitHub artifact** named `project-doc`. This allows the documentation to be stored and accessed after workflow runs.