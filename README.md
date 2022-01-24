
## github-git-log

Someone else must have written this already but i can't find it, so here it is.

`github-git-log [options] https://github.com/user/repo`

Remote git log for github

git doesn't handle viewing commits of remote repos. Normally you have to clone the repo first.

This tool shows the commit history of a remote git repository hosted on github without cloning it.
Saves quite a bit of time and bandwidth if the repo is huge and you only care about the commit
history.

Uses the github rest api to get repo data, so only works for github right now.
Supporting others shouldn't be too hard if they also have a rest api.

**Notes:**
- only works for the default branch.  
  doesn't seem the api provides a good way to query other branches, investigate ...
- use `--tags` to display tags
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

**Demo:**
```
$ github-git-log -t "https://github.com/torvalds/linux" | less -S
           Linus Torvalds dd81e1c7d 2022-01-23                    Merge tag 'powerpc-5.17-2' of git://git.kernel.org/pub/scm/linux/kernel/git/powerpc/linux
           Linus Torvalds ac5a9bb6b 2022-01-23                    Merge tag 'irq_urgent_for_v5.17_rc2' of git://git.kernel.org/pub/scm/linux/kernel/git/tip/tip
           Linus Torvalds 10c64a0f2 2022-01-23                    Merge tag 'sched_urgent_for_v5.17_rc2' of git://git.kernel.org/pub/scm/linux/kernel/git/tip/tip
           Linus Torvalds 0f9e04221 2022-01-23                    Merge tag 'perf_urgent_for_v5.17_rc2' of git://git.kernel.org/pub/scm/linux/kernel/git/tip/tip
           Linus Torvalds e783362eb 2022-01-23 v5.17-rc1^{}       Linux 5.17-rc1
           Linus Torvalds 40c843218 2022-01-23                    Merge tag 'perf-tools-for-v5.17-2022-01-22' of git://git.kernel.org/pub/scm/linux/kernel/git/acme/linux
           Linus Torvalds 67bfce0e0 2022-01-23                    Merge tag 'trace-v5.17-3' of git://git.kernel.org/pub/scm/linux/kernel/git/rostedt/linux-trace
          Steven Rostedt  6b9b64137 2022-01-22                    ftrace: Fix assuming build time sort works for s390
           Linus Torvalds 473aec0e1 2022-01-23                    Merge tag 'kbuild-fixes-v5.17' of git://git.kernel.org/pub/scm/linux/kernel/git/masahiroy/linux-kbuild
           Linus Torvalds 3689f9f8b 2022-01-23                    Merge tag 'bitmap-5.17-rc1' of git://github.com/norov/linux
              Minghao Chi f0ac5b858 2022-01-12                    perf tools: Remove redundant err variable
               John Garry b4a7276c5 2022-01-17                    perf test: Add parse-events test for aliases with hyphens
               John Garry 34fa67e72 2022-01-17                    perf test: Add pmu-events test for aliases with hyphens
               John Garry 864bc8c90 2022-01-17                    perf parse-events: Support event alias in form foo-bar-baz
             German Gomez 3606c0e1a 2022-01-18                    perf evsel: Override attr->sample_period for non-libpfm4 events
                  Lv Ruyi 24ead7c25 2022-01-17                    perf cpumap: Remove duplicate include in cpumap.h
               Ian Rogers 440286993 2022-01-22                    perf cpumap: Migrate to libperf cpumap api
               Ian Rogers 1d1d9af25 2022-01-22                    perf python: Fix cpu_map__item() building
                  Yao Jin 9edcde68d 2022-01-21                    perf script: Fix printing 'phys_addr' failure issue
          Masahiro Yamada e6340b652 2022-01-20                    certs: Fix build error when CONFIG_MODULE_SIG_KEY is empty
          Masahiro Yamada ad29a2fb3 2022-01-20                    certs: Fix build error when CONFIG_MODULE_SIG_KEY is PKCS#11 URI
          Masahiro Yamada e92e2634e 2022-01-20                    Revert "Makefile: Do not quote value for CONFIG_CC_IMPLICIT_FALLTHROUGH"
          Dmitry V. Levin 10756dc5b 2022-01-03                    usr/include/Makefile: add linux/nfc.h to the compile-test coverage
           Linus Torvalds 1c5228326 2022-01-22                    Merge branch 'akpm' (patches from Andrew)
           Linus Torvalds 8205ae327 2022-01-22                    Merge tag '5.17-rc-part2-smb3-fixes' of git://git.samba.org/sfrench/cifs-2.6
           Linus Torvalds 1cb69c804 2022-01-22                    Merge tag 'xfs-5.17-merge-7' of git://git.kernel.org/pub/scm/fs/xfs/xfs-linux
           Linus Torvalds 7fd350f6f 2022-01-22                    Merge tag 'fscache-fixes-20220121' of git://git.kernel.org/pub/scm/linux/kernel/git/dhowells/linux-fs
           Linus Torvalds b68b10b62 2022-01-22                    Merge tag 'folio-5.17a' of git://git.infradead.org/users/willy/pagecache
           Linus Torvalds 369af20a2 2022-01-22                    Merge tag 'scsi-misc' of git://git.kernel.org/pub/scm/linux/kernel/git/jejb/scsi
           Linus Torvalds b087788c2 2022-01-22                    Merge tag 'ata-5.17-rc1-part2' of git://git.kernel.org/pub/scm/linux/kernel/git/dlemoal/libata
```