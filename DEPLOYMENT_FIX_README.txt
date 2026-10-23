GOLDFLOW AI ELITE — DEPLOYMENT FIX

The Dockerfile expects this repository-root layout:
  Dockerfile
  backend/requirements.txt
  backend/app.py
  frontend/index.html
  render.yaml

The Render log says the Docker build context transferred only 2 bytes and the COPY instructions could not find backend/ or frontend/. This indicates Render's build context is not receiving the repository files in the expected layout (commonly a wrong Root Directory, wrong connected repository/branch, or files not committed at the repository root). It is not fixed by changing the Dockerfile alone.

Render service settings:
- Root Directory: leave BLANK (repository root)
- Runtime: Docker
- Dockerfile Path: ./Dockerfile
- Build Context Directory: repository root, if this field is shown
- Branch: the branch containing these files (usually main)
- Save changes, then Manual Deploy → Deploy latest commit.

Do not upload this ZIP as a single file into GitHub and expect Docker to extract it. GitHub must contain the extracted files and folders at the repository root. This ZIP already contains the correctly structured source tree.

After deployment succeeds, open https://YOUR-RENDER-SERVICE.onrender.com/api/health.
A successful health response proves the service is running; it does not prove live market provider credentials are configured. Add provider API keys only in Render's Environment settings, never in GitHub.
