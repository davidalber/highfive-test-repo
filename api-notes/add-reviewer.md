1. Initial state.
```sh
$ http https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1/requested_reviewers
HTTP/1.1 200 OK
.
.
.
{
    "teams": [],
    "users": []
}
```

The PR has no assigned reviewers.

2. Attempting to add a non-collaborator reviewer.
```
$ http POST https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1/requested_reviewers Authorization:"token OAUTH_TOKEN" reviewers:='["blah"]'
HTTP/1.1 422 Unprocessable Entity
.
.
.
{
    "documentation_url": "https://developer.github.com/v3/pulls/review_requests/#create-a-review-request",
    "message": "Reviews may only be requested from collaborators. One or more of the users or teams you specified is not a collaborator of the davidalber/highfive-test-repo repository."
}
```

There's still no reviewer assigned:
```
{
    "teams": [],
    "users": []
}
```

3. Attempting to add PR creator as reviewer.
```
$ http POST https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1/requested_reviewers Authorization:"token OAUTH_TOKEN" reviewers:='["davidalber"]'
HTTP/1.1 422 Unprocessable Entity
.
.
.
{
    "documentation_url": "https://developer.github.com/v3/pulls/review_requests/#create-a-review-request",
    "message": "Review cannot be requested from pull request author."
}
```

There's still no reviewer assigned:
```
{
    "teams": [],
    "users": []
}
```

4. Adding a collaborator reviewer.
```
$ http POST https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1/requested_reviewers Authorization:"token OAUTH_TOKEN" reviewers:='["TapscottLab"]'
HTTP/1.1 201 Created
.
.
.
{
   "url":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1",
   "id":174553582,
   "html_url":"https://github.com/davidalber/highfive-test-repo/pull/1",
   "diff_url":"https://github.com/davidalber/highfive-test-repo/pull/1.diff",
   "patch_url":"https://github.com/davidalber/highfive-test-repo/pull/1.patch",
   "issue_url":"https://api.github.com/repos/davidalber/highfive-test-repo/issues/1",
   "number":1,
   "state":"open",
   "locked":false,
   "title":"Add notes on requesting and setting reviewers",
   "user":{
      "login":"davidalber",
      "id":933552,
      "avatar_url":"https://avatars3.githubusercontent.com/u/933552?v=4",
      "gravatar_id":"",
      "url":"https://api.github.com/users/davidalber",
      "html_url":"https://github.com/davidalber",
      "followers_url":"https://api.github.com/users/davidalber/followers",
      "following_url":"https://api.github.com/users/davidalber/following{/other_user}",
      "gists_url":"https://api.github.com/users/davidalber/gists{/gist_id}",
      "starred_url":"https://api.github.com/users/davidalber/starred{/owner}{/repo}",
      "subscriptions_url":"https://api.github.com/users/davidalber/subscriptions",
      "organizations_url":"https://api.github.com/users/davidalber/orgs",
      "repos_url":"https://api.github.com/users/davidalber/repos",
      "events_url":"https://api.github.com/users/davidalber/events{/privacy}",
      "received_events_url":"https://api.github.com/users/davidalber/received_events",
      "type":"User",
      "site_admin":false
   },
   "body":"This PR adds notes on using the GitHub API to manipulate and query [review requests](https://developer.github.com/v3/pulls/review_requests/).",
   "created_at":"2018-03-13T04:09:56Z",
   "updated_at":"2018-03-13T04:33:04Z",
   "closed_at":null,
   "merged_at":null,
   "merge_commit_sha":"8eb36a6f5672b5fa192c31c95ed7f7ec29ad1e8a",
   "assignee":null,
   "assignees":[

   ],
   "requested_reviewers":[
      {
         "login":"TapscottLab",
         "id":22222483,
         "avatar_url":"https://avatars2.githubusercontent.com/u/22222483?v=4",
         "gravatar_id":"",
         "url":"https://api.github.com/users/TapscottLab",
         "html_url":"https://github.com/TapscottLab",
         "followers_url":"https://api.github.com/users/TapscottLab/followers",
         "following_url":"https://api.github.com/users/TapscottLab/following{/other_user}",
         "gists_url":"https://api.github.com/users/TapscottLab/gists{/gist_id}",
         "starred_url":"https://api.github.com/users/TapscottLab/starred{/owner}{/repo}",
         "subscriptions_url":"https://api.github.com/users/TapscottLab/subscriptions",
         "organizations_url":"https://api.github.com/users/TapscottLab/orgs",
         "repos_url":"https://api.github.com/users/TapscottLab/repos",
         "events_url":"https://api.github.com/users/TapscottLab/events{/privacy}",
         "received_events_url":"https://api.github.com/users/TapscottLab/received_events",
         "type":"User",
         "site_admin":false
      }
   ],
   "requested_teams":[

   ],
   "labels":[

   ],
   "milestone":null,
   "commits_url":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1/commits",
   "review_comments_url":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1/comments",
   "review_comment_url":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls/comments{/number}",
   "comments_url":"https://api.github.com/repos/davidalber/highfive-test-repo/issues/1/comments",
   "statuses_url":"https://api.github.com/repos/davidalber/highfive-test-repo/statuses/20811ae97ad2d3f01ec88d64d3d4f7a6b0c783bc",
   "head":{
      "label":"davidalber:add-reviewer",
      "ref":"add-reviewer",
      "sha":"20811ae97ad2d3f01ec88d64d3d4f7a6b0c783bc",
      "user":{
         "login":"davidalber",
         "id":933552,
         "avatar_url":"https://avatars3.githubusercontent.com/u/933552?v=4",
         "gravatar_id":"",
         "url":"https://api.github.com/users/davidalber",
         "html_url":"https://github.com/davidalber",
         "followers_url":"https://api.github.com/users/davidalber/followers",
         "following_url":"https://api.github.com/users/davidalber/following{/other_user}",
         "gists_url":"https://api.github.com/users/davidalber/gists{/gist_id}",
         "starred_url":"https://api.github.com/users/davidalber/starred{/owner}{/repo}",
         "subscriptions_url":"https://api.github.com/users/davidalber/subscriptions",
         "organizations_url":"https://api.github.com/users/davidalber/orgs",
         "repos_url":"https://api.github.com/users/davidalber/repos",
         "events_url":"https://api.github.com/users/davidalber/events{/privacy}",
         "received_events_url":"https://api.github.com/users/davidalber/received_events",
         "type":"User",
         "site_admin":false
      },
      "repo":{
         "id":124983756,
         "name":"highfive-test-repo",
         "full_name":"davidalber/highfive-test-repo",
         "owner":{
            "login":"davidalber",
            "id":933552,
            "avatar_url":"https://avatars3.githubusercontent.com/u/933552?v=4",
            "gravatar_id":"",
            "url":"https://api.github.com/users/davidalber",
            "html_url":"https://github.com/davidalber",
            "followers_url":"https://api.github.com/users/davidalber/followers",
            "following_url":"https://api.github.com/users/davidalber/following{/other_user}",
            "gists_url":"https://api.github.com/users/davidalber/gists{/gist_id}",
            "starred_url":"https://api.github.com/users/davidalber/starred{/owner}{/repo}",
            "subscriptions_url":"https://api.github.com/users/davidalber/subscriptions",
            "organizations_url":"https://api.github.com/users/davidalber/orgs",
            "repos_url":"https://api.github.com/users/davidalber/repos",
            "events_url":"https://api.github.com/users/davidalber/events{/privacy}",
            "received_events_url":"https://api.github.com/users/davidalber/received_events",
            "type":"User",
            "site_admin":false
         },
         "private":false,
         "html_url":"https://github.com/davidalber/highfive-test-repo",
         "description":"A repository for testing Highfive.",
         "fork":false,
         "url":"https://api.github.com/repos/davidalber/highfive-test-repo",
         "forks_url":"https://api.github.com/repos/davidalber/highfive-test-repo/forks",
         "keys_url":"https://api.github.com/repos/davidalber/highfive-test-repo/keys{/key_id}",
         "collaborators_url":"https://api.github.com/repos/davidalber/highfive-test-repo/collaborators{/collaborator}",
         "teams_url":"https://api.github.com/repos/davidalber/highfive-test-repo/teams",
         "hooks_url":"https://api.github.com/repos/davidalber/highfive-test-repo/hooks",
         "issue_events_url":"https://api.github.com/repos/davidalber/highfive-test-repo/issues/events{/number}",
         "events_url":"https://api.github.com/repos/davidalber/highfive-test-repo/events",
         "assignees_url":"https://api.github.com/repos/davidalber/highfive-test-repo/assignees{/user}",
         "branches_url":"https://api.github.com/repos/davidalber/highfive-test-repo/branches{/branch}",
         "tags_url":"https://api.github.com/repos/davidalber/highfive-test-repo/tags",
         "blobs_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/blobs{/sha}",
         "git_tags_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/tags{/sha}",
         "git_refs_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/refs{/sha}",
         "trees_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/trees{/sha}",
         "statuses_url":"https://api.github.com/repos/davidalber/highfive-test-repo/statuses/{sha}",
         "languages_url":"https://api.github.com/repos/davidalber/highfive-test-repo/languages",
         "stargazers_url":"https://api.github.com/repos/davidalber/highfive-test-repo/stargazers",
         "contributors_url":"https://api.github.com/repos/davidalber/highfive-test-repo/contributors",
         "subscribers_url":"https://api.github.com/repos/davidalber/highfive-test-repo/subscribers",
         "subscription_url":"https://api.github.com/repos/davidalber/highfive-test-repo/subscription",
         "commits_url":"https://api.github.com/repos/davidalber/highfive-test-repo/commits{/sha}",
         "git_commits_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/commits{/sha}",
         "comments_url":"https://api.github.com/repos/davidalber/highfive-test-repo/comments{/number}",
         "issue_comment_url":"https://api.github.com/repos/davidalber/highfive-test-repo/issues/comments{/number}",
         "contents_url":"https://api.github.com/repos/davidalber/highfive-test-repo/contents/{+path}",
         "compare_url":"https://api.github.com/repos/davidalber/highfive-test-repo/compare/{base}...{head}",
         "merges_url":"https://api.github.com/repos/davidalber/highfive-test-repo/merges",
         "archive_url":"https://api.github.com/repos/davidalber/highfive-test-repo/{archive_format}{/ref}",
         "downloads_url":"https://api.github.com/repos/davidalber/highfive-test-repo/downloads",
         "issues_url":"https://api.github.com/repos/davidalber/highfive-test-repo/issues{/number}",
         "pulls_url":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls{/number}",
         "milestones_url":"https://api.github.com/repos/davidalber/highfive-test-repo/milestones{/number}",
         "notifications_url":"https://api.github.com/repos/davidalber/highfive-test-repo/notifications{?since,all,participating}",
         "labels_url":"https://api.github.com/repos/davidalber/highfive-test-repo/labels{/name}",
         "releases_url":"https://api.github.com/repos/davidalber/highfive-test-repo/releases{/id}",
         "deployments_url":"https://api.github.com/repos/davidalber/highfive-test-repo/deployments",
         "created_at":"2018-03-13T02:59:19Z",
         "updated_at":"2018-03-13T02:59:19Z",
         "pushed_at":"2018-03-13T04:09:57Z",
         "git_url":"git://github.com/davidalber/highfive-test-repo.git",
         "ssh_url":"git@github.com:davidalber/highfive-test-repo.git",
         "clone_url":"https://github.com/davidalber/highfive-test-repo.git",
         "svn_url":"https://github.com/davidalber/highfive-test-repo",
         "homepage":null,
         "size":0,
         "stargazers_count":0,
         "watchers_count":0,
         "language":null,
         "has_issues":true,
         "has_projects":true,
         "has_downloads":true,
         "has_wiki":true,
         "has_pages":false,
         "forks_count":0,
         "mirror_url":null,
         "archived":false,
         "open_issues_count":1,
         "license":null,
         "forks":0,
         "open_issues":1,
         "watchers":0,
         "default_branch":"master"
      }
   },
   "base":{
      "label":"davidalber:master",
      "ref":"master",
      "sha":"411a1d66197278c4d0bfc09a95cee84440009319",
      "user":{
         "login":"davidalber",
         "id":933552,
         "avatar_url":"https://avatars3.githubusercontent.com/u/933552?v=4",
         "gravatar_id":"",
         "url":"https://api.github.com/users/davidalber",
         "html_url":"https://github.com/davidalber",
         "followers_url":"https://api.github.com/users/davidalber/followers",
         "following_url":"https://api.github.com/users/davidalber/following{/other_user}",
         "gists_url":"https://api.github.com/users/davidalber/gists{/gist_id}",
         "starred_url":"https://api.github.com/users/davidalber/starred{/owner}{/repo}",
         "subscriptions_url":"https://api.github.com/users/davidalber/subscriptions",
         "organizations_url":"https://api.github.com/users/davidalber/orgs",
         "repos_url":"https://api.github.com/users/davidalber/repos",
         "events_url":"https://api.github.com/users/davidalber/events{/privacy}",
         "received_events_url":"https://api.github.com/users/davidalber/received_events",
         "type":"User",
         "site_admin":false
      },
      "repo":{
         "id":124983756,
         "name":"highfive-test-repo",
         "full_name":"davidalber/highfive-test-repo",
         "owner":{
            "login":"davidalber",
            "id":933552,
            "avatar_url":"https://avatars3.githubusercontent.com/u/933552?v=4",
            "gravatar_id":"",
            "url":"https://api.github.com/users/davidalber",
            "html_url":"https://github.com/davidalber",
            "followers_url":"https://api.github.com/users/davidalber/followers",
            "following_url":"https://api.github.com/users/davidalber/following{/other_user}",
            "gists_url":"https://api.github.com/users/davidalber/gists{/gist_id}",
            "starred_url":"https://api.github.com/users/davidalber/starred{/owner}{/repo}",
            "subscriptions_url":"https://api.github.com/users/davidalber/subscriptions",
            "organizations_url":"https://api.github.com/users/davidalber/orgs",
            "repos_url":"https://api.github.com/users/davidalber/repos",
            "events_url":"https://api.github.com/users/davidalber/events{/privacy}",
            "received_events_url":"https://api.github.com/users/davidalber/received_events",
            "type":"User",
            "site_admin":false
         },
         "private":false,
         "html_url":"https://github.com/davidalber/highfive-test-repo",
         "description":"A repository for testing Highfive.",
         "fork":false,
         "url":"https://api.github.com/repos/davidalber/highfive-test-repo",
         "forks_url":"https://api.github.com/repos/davidalber/highfive-test-repo/forks",
         "keys_url":"https://api.github.com/repos/davidalber/highfive-test-repo/keys{/key_id}",
         "collaborators_url":"https://api.github.com/repos/davidalber/highfive-test-repo/collaborators{/collaborator}",
         "teams_url":"https://api.github.com/repos/davidalber/highfive-test-repo/teams",
         "hooks_url":"https://api.github.com/repos/davidalber/highfive-test-repo/hooks",
         "issue_events_url":"https://api.github.com/repos/davidalber/highfive-test-repo/issues/events{/number}",
         "events_url":"https://api.github.com/repos/davidalber/highfive-test-repo/events",
         "assignees_url":"https://api.github.com/repos/davidalber/highfive-test-repo/assignees{/user}",
         "branches_url":"https://api.github.com/repos/davidalber/highfive-test-repo/branches{/branch}",
         "tags_url":"https://api.github.com/repos/davidalber/highfive-test-repo/tags",
         "blobs_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/blobs{/sha}",
         "git_tags_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/tags{/sha}",
         "git_refs_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/refs{/sha}",
         "trees_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/trees{/sha}",
         "statuses_url":"https://api.github.com/repos/davidalber/highfive-test-repo/statuses/{sha}",
         "languages_url":"https://api.github.com/repos/davidalber/highfive-test-repo/languages",
         "stargazers_url":"https://api.github.com/repos/davidalber/highfive-test-repo/stargazers",
         "contributors_url":"https://api.github.com/repos/davidalber/highfive-test-repo/contributors",
         "subscribers_url":"https://api.github.com/repos/davidalber/highfive-test-repo/subscribers",
         "subscription_url":"https://api.github.com/repos/davidalber/highfive-test-repo/subscription",
         "commits_url":"https://api.github.com/repos/davidalber/highfive-test-repo/commits{/sha}",
         "git_commits_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/commits{/sha}",
         "comments_url":"https://api.github.com/repos/davidalber/highfive-test-repo/comments{/number}",
         "issue_comment_url":"https://api.github.com/repos/davidalber/highfive-test-repo/issues/comments{/number}",
         "contents_url":"https://api.github.com/repos/davidalber/highfive-test-repo/contents/{+path}",
         "compare_url":"https://api.github.com/repos/davidalber/highfive-test-repo/compare/{base}...{head}",
         "merges_url":"https://api.github.com/repos/davidalber/highfive-test-repo/merges",
         "archive_url":"https://api.github.com/repos/davidalber/highfive-test-repo/{archive_format}{/ref}",
         "downloads_url":"https://api.github.com/repos/davidalber/highfive-test-repo/downloads",
         "issues_url":"https://api.github.com/repos/davidalber/highfive-test-repo/issues{/number}",
         "pulls_url":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls{/number}",
         "milestones_url":"https://api.github.com/repos/davidalber/highfive-test-repo/milestones{/number}",
         "notifications_url":"https://api.github.com/repos/davidalber/highfive-test-repo/notifications{?since,all,participating}",
         "labels_url":"https://api.github.com/repos/davidalber/highfive-test-repo/labels{/name}",
         "releases_url":"https://api.github.com/repos/davidalber/highfive-test-repo/releases{/id}",
         "deployments_url":"https://api.github.com/repos/davidalber/highfive-test-repo/deployments",
         "created_at":"2018-03-13T02:59:19Z",
         "updated_at":"2018-03-13T02:59:19Z",
         "pushed_at":"2018-03-13T04:09:57Z",
         "git_url":"git://github.com/davidalber/highfive-test-repo.git",
         "ssh_url":"git@github.com:davidalber/highfive-test-repo.git",
         "clone_url":"https://github.com/davidalber/highfive-test-repo.git",
         "svn_url":"https://github.com/davidalber/highfive-test-repo",
         "homepage":null,
         "size":0,
         "stargazers_count":0,
         "watchers_count":0,
         "language":null,
         "has_issues":true,
         "has_projects":true,
         "has_downloads":true,
         "has_wiki":true,
         "has_pages":false,
         "forks_count":0,
         "mirror_url":null,
         "archived":false,
         "open_issues_count":1,
         "license":null,
         "forks":0,
         "open_issues":1,
         "watchers":0,
         "default_branch":"master"
      }
   },
   "_links":{
      "self":{
         "href":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1"
      },
      "html":{
         "href":"https://github.com/davidalber/highfive-test-repo/pull/1"
      },
      "issue":{
         "href":"https://api.github.com/repos/davidalber/highfive-test-repo/issues/1"
      },
      "comments":{
         "href":"https://api.github.com/repos/davidalber/highfive-test-repo/issues/1/comments"
      },
      "review_comments":{
         "href":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1/comments"
      },
      "review_comment":{
         "href":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls/comments{/number}"
      },
      "commits":{
         "href":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1/commits"
      },
      "statuses":{
         "href":"https://api.github.com/repos/davidalber/highfive-test-repo/statuses/20811ae97ad2d3f01ec88d64d3d4f7a6b0c783bc"
      }
   },
   "author_association":"OWNER"
}
```

There's now an assigned reviewer:
```
{
    "teams": [],
    "users": [
        {
            "avatar_url": "https://avatars2.githubusercontent.com/u/22222483?v=4",
            "events_url": "https://api.github.com/users/TapscottLab/events{/privacy}",
            "followers_url": "https://api.github.com/users/TapscottLab/followers",
            "following_url": "https://api.github.com/users/TapscottLab/following{/other_user}",
            "gists_url": "https://api.github.com/users/TapscottLab/gists{/gist_id}",
            "gravatar_id": "",
            "html_url": "https://github.com/TapscottLab",
            "id": 22222483,
            "login": "TapscottLab",
            "organizations_url": "https://api.github.com/users/TapscottLab/orgs",
            "received_events_url": "https://api.github.com/users/TapscottLab/received_events",
            "repos_url": "https://api.github.com/users/TapscottLab/repos",
            "site_admin": false,
            "starred_url": "https://api.github.com/users/TapscottLab/starred{/owner}{/repo}",
            "subscriptions_url": "https://api.github.com/users/TapscottLab/subscriptions",
            "type": "User",
            "url": "https://api.github.com/users/TapscottLab"
        }
    ]
}
```

5. Adding a collaborator reviewer a second time.
```
$ http POST https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1/requested_reviewers Authorization:"token OAUTH_TOKEN" reviewers:='["TapscottLab"]'
HTTP/1.1 201 Created
.
.
.
(it works as above)
```

There's still the same assigned reviewer:
```
(same as above)
```

6. Adding a different collaborator.
```sh
$ http POST https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1/requested_reviewers Authorization:"token OAUTH_TOKEN" reviewers:='["magillj"]'
```

```json
{
   "url":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1",
   "id":174553582,
   "html_url":"https://github.com/davidalber/highfive-test-repo/pull/1",
   "diff_url":"https://github.com/davidalber/highfive-test-repo/pull/1.diff",
   "patch_url":"https://github.com/davidalber/highfive-test-repo/pull/1.patch",
   "issue_url":"https://api.github.com/repos/davidalber/highfive-test-repo/issues/1",
   "number":1,
   "state":"open",
   "locked":false,
   "title":"Add notes on requesting and setting reviewers",
   "user":{
      "login":"davidalber",
      "id":933552,
      "avatar_url":"https://avatars3.githubusercontent.com/u/933552?v=4",
      "gravatar_id":"",
      "url":"https://api.github.com/users/davidalber",
      "html_url":"https://github.com/davidalber",
      "followers_url":"https://api.github.com/users/davidalber/followers",
      "following_url":"https://api.github.com/users/davidalber/following{/other_user}",
      "gists_url":"https://api.github.com/users/davidalber/gists{/gist_id}",
      "starred_url":"https://api.github.com/users/davidalber/starred{/owner}{/repo}",
      "subscriptions_url":"https://api.github.com/users/davidalber/subscriptions",
      "organizations_url":"https://api.github.com/users/davidalber/orgs",
      "repos_url":"https://api.github.com/users/davidalber/repos",
      "events_url":"https://api.github.com/users/davidalber/events{/privacy}",
      "received_events_url":"https://api.github.com/users/davidalber/received_events",
      "type":"User",
      "site_admin":false
   },
   "body":"This PR adds notes on using the GitHub API to manipulate and query [review requests](https://developer.github.com/v3/pulls/review_requests/).",
   "created_at":"2018-03-13T04:09:56Z",
   "updated_at":"2018-03-15T04:31:17Z",
   "closed_at":null,
   "merged_at":null,
   "merge_commit_sha":"7ca4b6d5cb23e4ea94396a82be23a717a3486d73",
   "assignee":null,
   "assignees":[

   ],
   "requested_reviewers":[
      {
         "login":"magillj",
         "id":7777180,
         "avatar_url":"https://avatars0.githubusercontent.com/u/7777180?v=4",
         "gravatar_id":"",
         "url":"https://api.github.com/users/magillj",
         "html_url":"https://github.com/magillj",
         "followers_url":"https://api.github.com/users/magillj/followers",
         "following_url":"https://api.github.com/users/magillj/following{/other_user}",
         "gists_url":"https://api.github.com/users/magillj/gists{/gist_id}",
         "starred_url":"https://api.github.com/users/magillj/starred{/owner}{/repo}",
         "subscriptions_url":"https://api.github.com/users/magillj/subscriptions",
         "organizations_url":"https://api.github.com/users/magillj/orgs",
         "repos_url":"https://api.github.com/users/magillj/repos",
         "events_url":"https://api.github.com/users/magillj/events{/privacy}",
         "received_events_url":"https://api.github.com/users/magillj/received_events",
         "type":"User",
         "site_admin":false
      },
      {
         "login":"TapscottLab",
         "id":22222483,
         "avatar_url":"https://avatars2.githubusercontent.com/u/22222483?v=4",
         "gravatar_id":"",
         "url":"https://api.github.com/users/TapscottLab",
         "html_url":"https://github.com/TapscottLab",
         "followers_url":"https://api.github.com/users/TapscottLab/followers",
         "following_url":"https://api.github.com/users/TapscottLab/following{/other_user}",
         "gists_url":"https://api.github.com/users/TapscottLab/gists{/gist_id}",
         "starred_url":"https://api.github.com/users/TapscottLab/starred{/owner}{/repo}",
         "subscriptions_url":"https://api.github.com/users/TapscottLab/subscriptions",
         "organizations_url":"https://api.github.com/users/TapscottLab/orgs",
         "repos_url":"https://api.github.com/users/TapscottLab/repos",
         "events_url":"https://api.github.com/users/TapscottLab/events{/privacy}",
         "received_events_url":"https://api.github.com/users/TapscottLab/received_events",
         "type":"User",
         "site_admin":false
      }
   ],
   "requested_teams":[

   ],
   "labels":[

   ],
   "milestone":null,
   "commits_url":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1/commits",
   "review_comments_url":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1/comments",
   "review_comment_url":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls/comments{/number}",
   "comments_url":"https://api.github.com/repos/davidalber/highfive-test-repo/issues/1/comments",
   "statuses_url":"https://api.github.com/repos/davidalber/highfive-test-repo/statuses/663682f343e944c01b2e8a3391d6ba5e6fe0339d",
   "head":{
      "label":"davidalber:add-reviewer",
      "ref":"add-reviewer",
      "sha":"663682f343e944c01b2e8a3391d6ba5e6fe0339d",
      "user":{
         "login":"davidalber",
         "id":933552,
         "avatar_url":"https://avatars3.githubusercontent.com/u/933552?v=4",
         "gravatar_id":"",
         "url":"https://api.github.com/users/davidalber",
         "html_url":"https://github.com/davidalber",
         "followers_url":"https://api.github.com/users/davidalber/followers",
         "following_url":"https://api.github.com/users/davidalber/following{/other_user}",
         "gists_url":"https://api.github.com/users/davidalber/gists{/gist_id}",
         "starred_url":"https://api.github.com/users/davidalber/starred{/owner}{/repo}",
         "subscriptions_url":"https://api.github.com/users/davidalber/subscriptions",
         "organizations_url":"https://api.github.com/users/davidalber/orgs",
         "repos_url":"https://api.github.com/users/davidalber/repos",
         "events_url":"https://api.github.com/users/davidalber/events{/privacy}",
         "received_events_url":"https://api.github.com/users/davidalber/received_events",
         "type":"User",
         "site_admin":false
      },
      "repo":{
         "id":124983756,
         "name":"highfive-test-repo",
         "full_name":"davidalber/highfive-test-repo",
         "owner":{
            "login":"davidalber",
            "id":933552,
            "avatar_url":"https://avatars3.githubusercontent.com/u/933552?v=4",
            "gravatar_id":"",
            "url":"https://api.github.com/users/davidalber",
            "html_url":"https://github.com/davidalber",
            "followers_url":"https://api.github.com/users/davidalber/followers",
            "following_url":"https://api.github.com/users/davidalber/following{/other_user}",
            "gists_url":"https://api.github.com/users/davidalber/gists{/gist_id}",
            "starred_url":"https://api.github.com/users/davidalber/starred{/owner}{/repo}",
            "subscriptions_url":"https://api.github.com/users/davidalber/subscriptions",
            "organizations_url":"https://api.github.com/users/davidalber/orgs",
            "repos_url":"https://api.github.com/users/davidalber/repos",
            "events_url":"https://api.github.com/users/davidalber/events{/privacy}",
            "received_events_url":"https://api.github.com/users/davidalber/received_events",
            "type":"User",
            "site_admin":false
         },
         "private":false,
         "html_url":"https://github.com/davidalber/highfive-test-repo",
         "description":"A repository for testing Highfive.",
         "fork":false,
         "url":"https://api.github.com/repos/davidalber/highfive-test-repo",
         "forks_url":"https://api.github.com/repos/davidalber/highfive-test-repo/forks",
         "keys_url":"https://api.github.com/repos/davidalber/highfive-test-repo/keys{/key_id}",
         "collaborators_url":"https://api.github.com/repos/davidalber/highfive-test-repo/collaborators{/collaborator}",
         "teams_url":"https://api.github.com/repos/davidalber/highfive-test-repo/teams",
         "hooks_url":"https://api.github.com/repos/davidalber/highfive-test-repo/hooks",
         "issue_events_url":"https://api.github.com/repos/davidalber/highfive-test-repo/issues/events{/number}",
         "events_url":"https://api.github.com/repos/davidalber/highfive-test-repo/events",
         "assignees_url":"https://api.github.com/repos/davidalber/highfive-test-repo/assignees{/user}",
         "branches_url":"https://api.github.com/repos/davidalber/highfive-test-repo/branches{/branch}",
         "tags_url":"https://api.github.com/repos/davidalber/highfive-test-repo/tags",
         "blobs_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/blobs{/sha}",
         "git_tags_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/tags{/sha}",
         "git_refs_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/refs{/sha}",
         "trees_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/trees{/sha}",
         "statuses_url":"https://api.github.com/repos/davidalber/highfive-test-repo/statuses/{sha}",
         "languages_url":"https://api.github.com/repos/davidalber/highfive-test-repo/languages",
         "stargazers_url":"https://api.github.com/repos/davidalber/highfive-test-repo/stargazers",
         "contributors_url":"https://api.github.com/repos/davidalber/highfive-test-repo/contributors",
         "subscribers_url":"https://api.github.com/repos/davidalber/highfive-test-repo/subscribers",
         "subscription_url":"https://api.github.com/repos/davidalber/highfive-test-repo/subscription",
         "commits_url":"https://api.github.com/repos/davidalber/highfive-test-repo/commits{/sha}",
         "git_commits_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/commits{/sha}",
         "comments_url":"https://api.github.com/repos/davidalber/highfive-test-repo/comments{/number}",
         "issue_comment_url":"https://api.github.com/repos/davidalber/highfive-test-repo/issues/comments{/number}",
         "contents_url":"https://api.github.com/repos/davidalber/highfive-test-repo/contents/{+path}",
         "compare_url":"https://api.github.com/repos/davidalber/highfive-test-repo/compare/{base}...{head}",
         "merges_url":"https://api.github.com/repos/davidalber/highfive-test-repo/merges",
         "archive_url":"https://api.github.com/repos/davidalber/highfive-test-repo/{archive_format}{/ref}",
         "downloads_url":"https://api.github.com/repos/davidalber/highfive-test-repo/downloads",
         "issues_url":"https://api.github.com/repos/davidalber/highfive-test-repo/issues{/number}",
         "pulls_url":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls{/number}",
         "milestones_url":"https://api.github.com/repos/davidalber/highfive-test-repo/milestones{/number}",
         "notifications_url":"https://api.github.com/repos/davidalber/highfive-test-repo/notifications{?since,all,participating}",
         "labels_url":"https://api.github.com/repos/davidalber/highfive-test-repo/labels{/name}",
         "releases_url":"https://api.github.com/repos/davidalber/highfive-test-repo/releases{/id}",
         "deployments_url":"https://api.github.com/repos/davidalber/highfive-test-repo/deployments",
         "created_at":"2018-03-13T02:59:19Z",
         "updated_at":"2018-03-13T02:59:19Z",
         "pushed_at":"2018-03-13T15:37:05Z",
         "git_url":"git://github.com/davidalber/highfive-test-repo.git",
         "ssh_url":"git@github.com:davidalber/highfive-test-repo.git",
         "clone_url":"https://github.com/davidalber/highfive-test-repo.git",
         "svn_url":"https://github.com/davidalber/highfive-test-repo",
         "homepage":null,
         "size":4,
         "stargazers_count":0,
         "watchers_count":0,
         "language":null,
         "has_issues":true,
         "has_projects":true,
         "has_downloads":true,
         "has_wiki":true,
         "has_pages":false,
         "forks_count":0,
         "mirror_url":null,
         "archived":false,
         "open_issues_count":1,
         "license":null,
         "forks":0,
         "open_issues":1,
         "watchers":0,
         "default_branch":"master"
      }
   },
   "base":{
      "label":"davidalber:master",
      "ref":"master",
      "sha":"411a1d66197278c4d0bfc09a95cee84440009319",
      "user":{
         "login":"davidalber",
         "id":933552,
         "avatar_url":"https://avatars3.githubusercontent.com/u/933552?v=4",
         "gravatar_id":"",
         "url":"https://api.github.com/users/davidalber",
         "html_url":"https://github.com/davidalber",
         "followers_url":"https://api.github.com/users/davidalber/followers",
         "following_url":"https://api.github.com/users/davidalber/following{/other_user}",
         "gists_url":"https://api.github.com/users/davidalber/gists{/gist_id}",
         "starred_url":"https://api.github.com/users/davidalber/starred{/owner}{/repo}",
         "subscriptions_url":"https://api.github.com/users/davidalber/subscriptions",
         "organizations_url":"https://api.github.com/users/davidalber/orgs",
         "repos_url":"https://api.github.com/users/davidalber/repos",
         "events_url":"https://api.github.com/users/davidalber/events{/privacy}",
         "received_events_url":"https://api.github.com/users/davidalber/received_events",
         "type":"User",
         "site_admin":false
      },
      "repo":{
         "id":124983756,
         "name":"highfive-test-repo",
         "full_name":"davidalber/highfive-test-repo",
         "owner":{
            "login":"davidalber",
            "id":933552,
            "avatar_url":"https://avatars3.githubusercontent.com/u/933552?v=4",
            "gravatar_id":"",
            "url":"https://api.github.com/users/davidalber",
            "html_url":"https://github.com/davidalber",
            "followers_url":"https://api.github.com/users/davidalber/followers",
            "following_url":"https://api.github.com/users/davidalber/following{/other_user}",
            "gists_url":"https://api.github.com/users/davidalber/gists{/gist_id}",
            "starred_url":"https://api.github.com/users/davidalber/starred{/owner}{/repo}",
            "subscriptions_url":"https://api.github.com/users/davidalber/subscriptions",
            "organizations_url":"https://api.github.com/users/davidalber/orgs",
            "repos_url":"https://api.github.com/users/davidalber/repos",
            "events_url":"https://api.github.com/users/davidalber/events{/privacy}",
            "received_events_url":"https://api.github.com/users/davidalber/received_events",
            "type":"User",
            "site_admin":false
         },
         "private":false,
         "html_url":"https://github.com/davidalber/highfive-test-repo",
         "description":"A repository for testing Highfive.",
         "fork":false,
         "url":"https://api.github.com/repos/davidalber/highfive-test-repo",
         "forks_url":"https://api.github.com/repos/davidalber/highfive-test-repo/forks",
         "keys_url":"https://api.github.com/repos/davidalber/highfive-test-repo/keys{/key_id}",
         "collaborators_url":"https://api.github.com/repos/davidalber/highfive-test-repo/collaborators{/collaborator}",
         "teams_url":"https://api.github.com/repos/davidalber/highfive-test-repo/teams",
         "hooks_url":"https://api.github.com/repos/davidalber/highfive-test-repo/hooks",
         "issue_events_url":"https://api.github.com/repos/davidalber/highfive-test-repo/issues/events{/number}",
         "events_url":"https://api.github.com/repos/davidalber/highfive-test-repo/events",
         "assignees_url":"https://api.github.com/repos/davidalber/highfive-test-repo/assignees{/user}",
         "branches_url":"https://api.github.com/repos/davidalber/highfive-test-repo/branches{/branch}",
         "tags_url":"https://api.github.com/repos/davidalber/highfive-test-repo/tags",
         "blobs_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/blobs{/sha}",
         "git_tags_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/tags{/sha}",
         "git_refs_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/refs{/sha}",
         "trees_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/trees{/sha}",
         "statuses_url":"https://api.github.com/repos/davidalber/highfive-test-repo/statuses/{sha}",
         "languages_url":"https://api.github.com/repos/davidalber/highfive-test-repo/languages",
         "stargazers_url":"https://api.github.com/repos/davidalber/highfive-test-repo/stargazers",
         "contributors_url":"https://api.github.com/repos/davidalber/highfive-test-repo/contributors",
         "subscribers_url":"https://api.github.com/repos/davidalber/highfive-test-repo/subscribers",
         "subscription_url":"https://api.github.com/repos/davidalber/highfive-test-repo/subscription",
         "commits_url":"https://api.github.com/repos/davidalber/highfive-test-repo/commits{/sha}",
         "git_commits_url":"https://api.github.com/repos/davidalber/highfive-test-repo/git/commits{/sha}",
         "comments_url":"https://api.github.com/repos/davidalber/highfive-test-repo/comments{/number}",
         "issue_comment_url":"https://api.github.com/repos/davidalber/highfive-test-repo/issues/comments{/number}",
         "contents_url":"https://api.github.com/repos/davidalber/highfive-test-repo/contents/{+path}",
         "compare_url":"https://api.github.com/repos/davidalber/highfive-test-repo/compare/{base}...{head}",
         "merges_url":"https://api.github.com/repos/davidalber/highfive-test-repo/merges",
         "archive_url":"https://api.github.com/repos/davidalber/highfive-test-repo/{archive_format}{/ref}",
         "downloads_url":"https://api.github.com/repos/davidalber/highfive-test-repo/downloads",
         "issues_url":"https://api.github.com/repos/davidalber/highfive-test-repo/issues{/number}",
         "pulls_url":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls{/number}",
         "milestones_url":"https://api.github.com/repos/davidalber/highfive-test-repo/milestones{/number}",
         "notifications_url":"https://api.github.com/repos/davidalber/highfive-test-repo/notifications{?since,all,participating}",
         "labels_url":"https://api.github.com/repos/davidalber/highfive-test-repo/labels{/name}",
         "releases_url":"https://api.github.com/repos/davidalber/highfive-test-repo/releases{/id}",
         "deployments_url":"https://api.github.com/repos/davidalber/highfive-test-repo/deployments",
         "created_at":"2018-03-13T02:59:19Z",
         "updated_at":"2018-03-13T02:59:19Z",
         "pushed_at":"2018-03-13T15:37:05Z",
         "git_url":"git://github.com/davidalber/highfive-test-repo.git",
         "ssh_url":"git@github.com:davidalber/highfive-test-repo.git",
         "clone_url":"https://github.com/davidalber/highfive-test-repo.git",
         "svn_url":"https://github.com/davidalber/highfive-test-repo",
         "homepage":null,
         "size":4,
         "stargazers_count":0,
         "watchers_count":0,
         "language":null,
         "has_issues":true,
         "has_projects":true,
         "has_downloads":true,
         "has_wiki":true,
         "has_pages":false,
         "forks_count":0,
         "mirror_url":null,
         "archived":false,
         "open_issues_count":1,
         "license":null,
         "forks":0,
         "open_issues":1,
         "watchers":0,
         "default_branch":"master"
      }
   },
   "_links":{
      "self":{
         "href":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1"
      },
      "html":{
         "href":"https://github.com/davidalber/highfive-test-repo/pull/1"
      },
      "issue":{
         "href":"https://api.github.com/repos/davidalber/highfive-test-repo/issues/1"
      },
      "comments":{
         "href":"https://api.github.com/repos/davidalber/highfive-test-repo/issues/1/comments"
      },
      "review_comments":{
         "href":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1/comments"
      },
      "review_comment":{
         "href":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls/comments{/number}"
      },
      "commits":{
         "href":"https://api.github.com/repos/davidalber/highfive-test-repo/pulls/1/commits"
      },
      "statuses":{
         "href":"https://api.github.com/repos/davidalber/highfive-test-repo/statuses/663682f343e944c01b2e8a3391d6ba5e6fe0339d"
      }
   },
   "author_association":"OWNER"
}
```

Takeaway: setting a reviewer when reviewers already exist appends the
new reviewer, instead of replacing the current reviewers.
