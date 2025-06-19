name: Daily Commit

on:
  schedule:
    # Runs every day at 10:05 AM UTC (adjust if needed)
    - cron: '5 10 * * *'
  workflow_dispatch:

jobs:
  commit-job:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Modify file for commit - 24f2007422@ds.study.iitm.ac.in
        run: |
          echo "Last commit: $(date -u)" > daily-update.txt

      - name: Commit and Push Changes
        run: |
          git config user.name "github-actions[bot]"
          git config user.email "41898282+github-actions[bot]@users.noreply.github.com"
          git add daily-update.txt
          git commit -m "Daily commit: $(date -u)" || echo "No changes to commit"
          git push
