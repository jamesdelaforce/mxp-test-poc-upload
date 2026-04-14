# Acme Corp — CSP Sync Prompt
# Paste this into Claude (with Slack + Google Drive MCPs active) to trigger a sync.
# Takes ~60 seconds. Claude will read Slack, update the HTML, and save to Drive.

---

Sync the Acme Corp customer success plan. Do the following steps in order:

1. Search Slack for all messages in #acme-success that have a 📌 pushpin reaction:
   - Query: `has::pushpin: in:#acme-success`
   - Also search for: `has::rotating_light: in:#acme-success`
   - Also search for: `has::white_check_mark: in:#acme-success`
   - Also search for: `has::bulb: in:#acme-success`

2. For each reacted message, extract:
   - The message text (clean up Slack formatting, remove @mentions markup)
   - The emoji that was used as reaction
   - The author name
   - The date (formatted as "D Mon YYYY", e.g. "11 Apr 2026")
   - Map emojis: pushpin→📌, rotating_light→🚨, white_check_mark→✅, bulb→💡

3. Read the current index.html from Google Drive (file ID: REPLACE_WITH_DRIVE_FILE_ID)

4. Replace ONLY the PLAN_DATA object inside the <script> block with an updated version:
   - Update the `updates` array with the messages found (newest first, max 8)
   - Update `last_synced` to the current UTC time in ISO format
   - Update `status` if any 🚨 messages suggest the account is at risk
   - Leave all other fields (metrics, goals, milestones, stakeholders) unchanged

5. Save the updated HTML back to Google Drive, overwriting the same file.
   - File ID: REPLACE_WITH_DRIVE_FILE_ID
   - Keep the filename: acme-corp-success-plan.html

6. Confirm the sync is complete and show me a summary of what updates were published.
