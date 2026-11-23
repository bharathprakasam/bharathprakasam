# Setup and publishing guide

## 1. Create the profile repository
1. Sign in to GitHub and create a **public** repository named exactly your GitHub username.
2. Extract this ZIP.
3. Replace every `USERNAME` in `README.md` with your exact GitHub username.
4. Upload all project files to the repository root, preserving the folder structure.

## 2. Generate the card locally (Windows PowerShell)
Install Python 3.10+ and open PowerShell in the extracted folder:

```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
py -m pip install -r requirements.txt
$env:GITHUB_USERNAME="YOUR_GITHUB_USERNAME"
$env:DISPLAY_NAME="Bharath"
py scripts/generate_profile.py
```

Then commit and push using Git:

```powershell
git add .
git commit -m "Create premium GitHub profile"
git push
```

Or use GitHub's **Add file → Upload files** page if Git is not installed.

## 3. Add your own ASCII portrait (optional)
The project does not include your personal photo. Place a photo on your PC and run:

```powershell
py scripts/image_to_ascii.py "C:\path\to\your-photo.jpg" --width 54
py scripts/generate_profile.py
git add assets/
git commit -m "Add ASCII profile portrait"
git push
```

The conversion runs locally. Review the generated SVG before publishing; it will be public in your repository.

## 4. Enable automatic card updates
1. Repository → **Settings → Actions → General**.
2. Under Workflow permissions, select **Read and write permissions** and save.
3. Go to **Actions → Update profile card → Run workflow**.
4. It will also run daily.

The workflow uses GitHub's automatically supplied `GITHUB_TOKEN`; do not create or paste a personal access token.

## 5. Personalize
Edit README.md: replace `USERNAME`, your LinkedIn link, remove or replace the portfolio link, and update skills/About text to match your actual experience. Edit workflow environment variables to change tagline or location.

## Notes
- The card shows public repositories, total stars across up to the latest 100 public repositories, followers, and following.
- External README statistics widgets can be rate-limited or unavailable.
- Never publish passwords, tokens, private details, or photos you do not have permission to use.
