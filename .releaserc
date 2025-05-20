{
  "branches": [
    { "name": "master" }
  ], 
  "plugins": [
    "@semantic-release/commit-analyzer",
    "@semantic-release/release-notes-generator",
    [
      "@semantic-release/changelog",
      {
        "changelogFile": "CHANGELOG.md",
        "changelogTitle": "# Changelog\n\nAll notable changes to this project will be documented in this file."
      }
    ],
    [
      "semantic-release-github-pullrequest",
      {
        "title": "chore(release): ${nextRelease.version}",
        "message": "chore(release): ${nextRelease.version}\n\n${nextRelease.notes}",
        "base": "master",
        "branch": (context) => {
          const branch = `release-pr-v${context.nextRelease.version.replace(/\./g, '-')}`;
          console.log('[debug] Using branch:', branch);
          return branch;
        },
        "sign": true
      }
    ],
  ]
}
