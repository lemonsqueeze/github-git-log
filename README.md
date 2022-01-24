
## github-git-log

Usage:  `github-git-log [options] https://github.com/user/repo | less -S`

Remote git log for github

git doesn't handle viewing commits of remote repos. Normally you have to clone the repo first.

This tool shows the commit history of a remote git repository hosted on github without cloning it.
Saves quite a bit of time and bandwidth if the repo is huge and you only care about the commit
history.

Uses the github rest api to get repo data, so only works for github right now.
Supporting others shouldn't be too hard if they also have a rest api.

**Limitations:**
- only works for the default branch.  
  doesn't seem the api provides a good way to query other branches, investigate ...
- api returns 30 commits at a time, so can be slow if you need to go very far back.
- by default github [rate-limits](https://docs.github.com/en/rest/overview/resources-in-the-rest-api#rate-limiting)
  unauthenticated requests to 60 per-hour.  
  The limit is much higher if you use an access token to authenticate.  
  You can create a [personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)
  in your github account's settings:
  
    [https://github.com/settings/tokens](https://github.com/settings/tokens)     (Personal access tokens -> Generate new token)
  
  Don't give it any scope (default) so the app cannot do anything to your account or
  repositories. Once the token is generated just edit the script and enter the token at
  the top to make it run in authenticated mode.
