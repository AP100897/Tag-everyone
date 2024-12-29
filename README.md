name: Tag Everyone Command

on:
  issue_comment:
    types: [created] # Triggers when a new comment is added to an issue or PR

jobs:
  tag-everyone:
    runs-on: ubuntu-latest

    steps:
      - name: Check for "tag everyone" command
        if: contains(github.event.comment.body, '@tag-everyone')
        run: |
          echo "Notifying collaborators..."
          
      - name: Notify All Collaborators
        run: |
          # List of collaborators to notify
          echo "Tagging @user1 @user2 @user3"
          curl -X POST -H "Authorization: Bearer ${{ secrets.GITHUB_TOKEN }}" \
            -H "Content-Type: application/json" \
            -d '{"body": "Attention @user1 @user2 @user3"}' \
            "${{ github.event.issue.url }}/comments"
