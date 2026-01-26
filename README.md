# Mik's Scrolling Battle Text

A version of the classic Mik's Scrolling Battle Text working for TBC Anniversary

This is a quickfix for Mik's Scrolling Battle Text for WoW TBC. I'm not the original author.

## Automatic Releases

This repository automatically creates releases on GitHub and CurseForge when you push a version tag (e.g., `v1.0.2`).

### Setting up CurseForge Automatic Uploads

To enable automatic uploads to CurseForge, you need to configure the following GitHub Secrets:

1. **Get your CurseForge API Token:**
   - Go to https://authors.curseforge.com/account/api-tokens
   - Create a new API token
   - Copy the token

2. **Get your Project ID or Slug:**
   - You can use either:
     - **Project Slug**: The URL-friendly name (e.g., `mikscrollingbattletext-tbc-anniversary`)
       - Found in your project URL: `https://www.curseforge.com/wow/addons/mikscrollingbattletext-tbc-anniversary`
     - **Numeric Project ID**: The numeric ID (e.g., `1431196`)
       - Found in the project settings page or API responses
   - The workflow will automatically resolve slugs to IDs if needed

3. **Get the Game Version ID:**
   - For TBC Anniversary version 2.5.5, the game version ID is: **`14300`**
   - When you query the API, look for the `id` field (not `apiVersion`):
     ```bash
     curl -H "X-Api-Token: YOUR_API_TOKEN" \
       https://wow.curseforge.com/api/game/versions | python3 -m json.tool
     ```
     Example response:
     ```json
     {
         "id": 14300,
         "name": "2.5.5",
         "slug": "2-5-5"
     }
     ```
     Use the `id` value (14300) as your `CURSEFORGE_GAME_VERSION_ID`

4. **Add GitHub Secrets:**
   - Go to your repository → Settings → Secrets and variables → Actions
   - Add the following secrets:
     - `CURSEFORGE_API_TOKEN`: Your CurseForge API token
     - `CURSEFORGE_PROJECT_ID`: Your CurseForge project ID (e.g., `1431196` or `mikscrollingbattletext-tbc-anniversary`)
     - `CURSEFORGE_GAME_VERSION_ID`: The game version ID (e.g., `14300` for TBC Anniversary 2.5.5)

### Creating a Release

1. Update the version in `MikScrollingBattleText/MikScrollingBattleText.toc`
2. Update `changelog.txt` with the new changes
3. Commit and push your changes
4. Create and push a version tag:
   ```bash
   git tag v1.0.2
   git push origin v1.0.2
   ```

The GitHub Actions workflow will automatically:
- Create a GitHub Release
- Upload the release package to GitHub
- Upload the release to CurseForge (if secrets are configured)
