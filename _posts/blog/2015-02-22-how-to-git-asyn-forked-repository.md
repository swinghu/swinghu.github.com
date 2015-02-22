---
layout: post
title: git如何merge forked repository里的代码更新?
description: github fork原作者的项目后，github不会自动更新同步原作者的代码，github里forked后的项目，如何与原作者的代码更新？
category: blog
---

# git如何merge forked repository里的代码更新? #

原作者的库：https://github.com/h2o/h2o.git
我从kazuho处fork的项目：https://github.com/swinghu/h2o.git
我git clone 原作者的库后，原作者是一个非常勤快的人，通常一天有几十个commit，导致不同于原作者的库及时更新，所以要定时与原作者的库进行asyn。

那么git如何对forked 后的库，与原作者进行库的更新，以获取原作者的最新代码？

具体做法，有以下三步奏：

（1）添加一个新的远程repository，kazuho指代对应的仓库地址

git remote add kazuho http://github.com/kazuho/h2o.git

（2）获取本地仓库当前还没有的信息，将远程仓库download 下来，运行git fetch kazuho

git fetch kazuho

（3）进行合并，使用git merge命令进行库合并
git merge kazuho/master

进行合并后，查看已经存在的远程分支：

D:\gitworkspace\H2O\h2o>git remote -v

kazuho  git@github.com:h2o/h2o.git (fetch)
kazuho  git@github.com:h2o/h2o.git (push)
origin  git@github.com:swinghu/h2o.git (fetch)
origin  git@github.com:swinghu/h2o.git (push)


列出本地已经存在的分支 git branch 命令，参数用法

- git branch 不带参数：列出本地已经存在的分支
- git branch -r 列出远程分支
- git branch -a 列出本地分支和远程分支
- git branch newbranch 创建分支
- git branch -m | -M oldbranch newbranch 重命名分支
- git branch -d | -D branchname 删除branchname分支
- git branch -d -r branchname 删除远程branchname分支


D:\gitworkspace\H2O\h2o>git branch -a
* master
  remotes/kazuho/kazuho/accept-sigterm-in-main-thread
  remotes/kazuho/kazuho/add-missing-extern-to-globals
  remotes/kazuho/kazuho/bench/token_lookup
  remotes/kazuho/kazuho/cache
  remotes/kazuho/kazuho/cache-rwlock
  remotes/kazuho/kazuho/dirlisting
  remotes/kazuho/kazuho/draft-16
  remotes/kazuho/kazuho/experiments/libuv-network-and-file
  remotes/kazuho/kazuho/experiments/libuv-network-only
  remotes/kazuho/kazuho/experiments/no-libuv
  remotes/kazuho/kazuho/expr/chunked-decoder
  remotes/kazuho/kazuho/expr/connect
  remotes/kazuho/kazuho/expr/dual-life
  remotes/kazuho/kazuho/expr/e2e-test
  remotes/kazuho/kazuho/expr/fix-travis-revproxy
  remotes/kazuho/kazuho/expr/hpack-using-index
  remotes/kazuho/kazuho/expr/http2-by-default
  remotes/kazuho/kazuho/expr/http2-priority
  remotes/kazuho/kazuho/expr/inbuf-initial-size
  remotes/kazuho/kazuho/expr/ipv6
  remotes/kazuho/kazuho/expr/libdl
  remotes/kazuho/kazuho/expr/libuv-network-only/1.0.0
  remotes/kazuho/kazuho/expr/loopback-testing
  remotes/kazuho/kazuho/expr/max-connections
  remotes/kazuho/kazuho/expr/mime-types-as-part-of-file
  remotes/kazuho/kazuho/expr/path-based-config
  remotes/kazuho/kazuho/expr/proxy-keepalive
  remotes/kazuho/kazuho/expr/proxy/chunked-decoder
  remotes/kazuho/kazuho/expr/pulling-generator
  remotes/kazuho/kazuho/expr/revproxy
  remotes/kazuho/kazuho/expr/sni
  remotes/kazuho/kazuho/expr/travis-libuv
  remotes/kazuho/kazuho/expr/travis/install-nghttp2
  remotes/kazuho/kazuho/faster-travis
  remotes/kazuho/kazuho/fix-crash-in-recycling-allocator
  remotes/kazuho/kazuho/fix-example-server-using-evloop
  remotes/kazuho/kazuho/fix-ignored-header-names-in-log
  remotes/kazuho/kazuho/fix-reverse-proxy
  remotes/kazuho/kazuho/flatten-t-dir
  remotes/kazuho/kazuho/graceful-restart
  remotes/kazuho/kazuho/graceful-shutdown
  remotes/kazuho/kazuho/h2spec-v0.0.6
  remotes/kazuho/kazuho/headers-in-lowercase
  remotes/kazuho/kazuho/http2-dependency-2
  remotes/kazuho/kazuho/http2-is-done
  remotes/kazuho/kazuho/http2-timeout
  remotes/kazuho/kazuho/http2/dependency
  remotes/kazuho/kazuho/http2/optimize-locality
  remotes/kazuho/kazuho/interthread-messaging
  remotes/kazuho/kazuho/issues/105
  remotes/kazuho/kazuho/issues/128
  remotes/kazuho/kazuho/issues/132
  remotes/kazuho/kazuho/issues/135
  remotes/kazuho/kazuho/issues/135-first-shot
  remotes/kazuho/kazuho/issues/135-take-two
  remotes/kazuho/kazuho/issues/141
  remotes/kazuho/kazuho/issues/146
  remotes/kazuho/kazuho/issues/173
  remotes/kazuho/kazuho/issues/61
  remotes/kazuho/kazuho/issues/61-reopen
  remotes/kazuho/kazuho/issues/65
  remotes/kazuho/kazuho/issues/93
  remotes/kazuho/kazuho/issues/crash-on-large-post
  remotes/kazuho/kazuho/issues/pr-101-segv
  remotes/kazuho/kazuho/issues/test-timeout
  remotes/kazuho/kazuho/memgrind
  remotes/kazuho/kazuho/more-logging-directives
  remotes/kazuho/kazuho/multiple-cookie-headers-in-http2
  remotes/kazuho/kazuho/netbsd-kqueue
  remotes/kazuho/kazuho/no-vary-if-msie
  remotes/kazuho/kazuho/nvlist-parser
  remotes/kazuho/kazuho/ocsp
  remotes/kazuho/kazuho/optimize-travis-bootstrap
  remotes/kazuho/kazuho/parse-if-modified-since
  remotes/kazuho/kazuho/parse_authority_from_url
  remotes/kazuho/kazuho/pid-file
  remotes/kazuho/kazuho/post-size-limit
  remotes/kazuho/kazuho/pr/45
  remotes/kazuho/kazuho/push
  remotes/kazuho/kazuho/refactor-http2-error-handling
  remotes/kazuho/kazuho/refactor-travis-yml
  remotes/kazuho/kazuho/refactor-travis-yml-upgrade-nghttp2
  remotes/kazuho/kazuho/refactor/config
  remotes/kazuho/kazuho/refactor/hpack
  remotes/kazuho/kazuho/refactor/hpack-encoder
  remotes/kazuho/kazuho/refactor/http1client/reduce-copy
  remotes/kazuho/kazuho/refactor/no-abstraction-for-openssl
  remotes/kazuho/kazuho/regexp
  remotes/kazuho/kazuho/server-starter
  remotes/kazuho/kazuho/session-resumption
  remotes/kazuho/kazuho/session-resumption-libyrmcds
  remotes/kazuho/kazuho/simplify-proxy-config
  remotes/kazuho/kazuho/split-configurator
  remotes/kazuho/kazuho/split-external-ver-and-lib-ver
  remotes/kazuho/kazuho/split-unit-tests
  remotes/kazuho/kazuho/test
  remotes/kazuho/kazuho/tmp/last-libuv
  remotes/kazuho/kazuho/upgrade-nghttp2
  remotes/kazuho/kazuho/url-handling-functions
  remotes/kazuho/kazuho/yoml-with-filename
  remotes/kazuho/master
  remotes/kazuho/rel/v0.9.0
  remotes/kazuho/rel/v0.9.1
  remotes/kazuho/rel/v1.0.0
  remotes/kazuho/tmp54
  remotes/kazuho/tmp55
  remotes/origin/HEAD -> origin/master
  remotes/origin/kazuho/experiments/libuv-network-and-file
  remotes/origin/kazuho/experiments/libuv-network-only
  remotes/origin/kazuho/experiments/no-libuv
  remotes/origin/kazuho/expr/dual-life
  remotes/origin/kazuho/expr/libuv-network-only/1.0.0
  remotes/origin/kazuho/tmp/last-libuv
  remotes/origin/master

以上命令列出了h2o项目的所有分支。