---
layout: post
date: 2014-02-05 1:42 PM
title: rvm requirements/ brew doctor 
cover: 
---

**I told** myself, If I am able to solve my OpenSSL error in ``rvm requirements``, I will post t he solution up as the **first blog post** on my [upcoming blog](http://iam.cusx.io)

{% highlight ruby %}
oox:~ cusxio$ rvm requirements
Checking requirements for osx.
dyld: Library not loaded: @@HOMEBREW_CELLAR@@/openssl/1.0.1f/lib/libssl.1.0.0.dylib
  Referenced from: /usr/local/opt/openssl/bin/openssl
  Reason: image not found
Failed reading certificates path for '/usr/local/opt/openssl/bin/openssl' with return code: ().
RVM autolibs is now configured with mode '2' => 'check and stop if missing',
please run `rvm autolibs enable` to let RVM do its job or run and read `rvm autolibs [help]`
or visit https://rvm.io/rvm/autolibs for more information.
Requirements installation failed with status: 133.
{% endhighlight %}

This is the error, persistently bugging me over the past few days. If I do a quick ``brew link openssl --forced`` the error will be solved, however running a quick ``brew doctor`` will show that home-brew is not happy with the link.

