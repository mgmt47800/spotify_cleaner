# Spotify Data Cleaner

Clean personally identifiable information (PII) from your downloaded Spotify account data so you can use it safely for class projects. The project uses the [Faker](https://faker.readthedocs.io/) library to replace usernames, emails, names, birthdates, and similar fields with realistic fake values while keeping your data structure and analytics usefulness intact.

## Prerequisites

- **VS Code** ([download](https://code.visualstudio.com/))  
- **Python** 3.9 or newer  
- **Poetry** ([installation guide](https://python-poetry.org/docs/#installation))  
- **Jupyter in VS Code** – install the [Jupyter](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter) extension (or the [Python](https://marketplace.visualstudio.com/items?itemName=ms-python.python) extension, which includes Jupyter support)  
- Your **Spotify account data** export (request it from [Spotify’s privacy page](https://www.spotify.com/account/privacy/) and download the zip; then extract it into a folder named `Spotify Account Data` in this project directory)

## Setup

1. Clone this repository (or download it) and open the project folder in **VS Code** (File → Open Folder).
2. Install dependencies with Poetry (open a terminal in VS Code: Terminal → New Terminal):

   ```bash
   poetry install --extras notebook
   ```

   This installs Faker and Jupyter so you can run the notebook inside VS Code.
3. Select the Poetry environment as the Python interpreter:
   - Press `Ctrl+Shift+P` (Windows/Linux) or `Cmd+Shift+P` (macOS), run **Python: Select Interpreter**.
   - Choose the interpreter that shows your Poetry virtualenv (e.g. `./.venv` or `Poetry (spotify-data-cleaner)`).
4. Place your Spotify data in a folder named **`Spotify Account Data`** inside this project folder (same level as `Spotify_Data_Cleaner.ipynb`). The folder should contain the JSON files from your Spotify export (e.g. `Userdata.json`, `Identifiers.json`, `Follow.json`, playlists, streaming history, etc.).

## Usage

1. In VS Code, open **`Spotify_Data_Cleaner.ipynb`**. If prompted to select a kernel, choose the Poetry environment you selected in Setup.
2. Run all cells from top to bottom (use **Run All** in the notebook toolbar, or run each cell in order with **Shift+Enter**).

3. The notebook will:
   - Read data from `Spotify Account Data/`
   - Replace PII with Faker-generated values (same original value always maps to the same fake value across files)
   - Write cleaned files into **`Spotify_Account_Data_Cleaned/`** (your original folder is left unchanged)
   - Create a zip file whose name is a **random number** (e.g. `71234987833478823.zip`) containing the cleaned folder, so you can submit or share it without identifying yourself

4. The **last cell** prints a **summary of all changes** (which file, which field, old value → new value).

## What Gets Replaced

- **Userdata.json:** username, email, birthdate, gender, Facebook UID, account creation time  
- **Identifiers.json:** email (same replacement as in Userdata for consistency)  
- **Follow.json:** display names in “following” / “followed by” / “blocking” lists  
- **Inferences.json:** demographic age bands and gender segments (replaced with generic values)  
- **Playlist names:** first names detected in playlist titles (e.g. “Harper’s Favorites”) are replaced with fake first names  

Other files (e.g. streaming history, library, playlists content, payments) are copied unchanged so your dataset stays complete. The summary at the end of the notebook lists every replacement that was made.

## Output

- **`Spotify_Account_Data_Cleaned/`** – folder containing the cleaned JSON files  
- **`<random_number>.zip`** – zip archive of that folder, with a numeric filename (e.g. `71234987833478823.zip`) for anonymous submission  

For course use. Keep your original `Spotify Account Data` folder private; only share or submit the generated zip if your instructor allows it.
