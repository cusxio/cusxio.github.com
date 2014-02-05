---
layout: post
date: 2014-02-05 3:18 PM
title: rvm requirements/ brew doctor 
cover: 
---

**I told** myself, If I am able to solve my OpenSSL error in ``rvm requirements``, I will post t he solution up as the **first blog post** on my [upcoming blog](http://iam.cusx.io)


```bash
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
```

This is the error, persistently bugging me over the past few days. If I do a quick ``brew link openssl --forced`` the error will be solved, however running a quick ``brew doctor`` will show that home-brew is not happy with the link.

I filed for a bug in *rvm support* on GitHub, and was told that this is a homebrew bug. So I filled for [another bug](https://github.com/Homebrew/homebrew/issues/26367) at homebrew. I was quickly told by the mods that the issue has something to do with `install_name_tools` being out-of-dated, perhaps being overwritten by some other apps during installation such as **RailsInstaller**. After much tinkering around `install_name_tools` I found a solution. I posted the whole solution on [GitHub](http://github.com), but for the sake of this post, I'll copy the whole thing here.
___

**Solution: Mavericks**

***PS: You need to install Command Line Tools (CLT)***

After installing command line tools, I realised that it is not located ``/Applications/Xcode.app/Contents/Developer/Tools``, the ~supposed to be~ directory.

1) Therefore, I quickly ran ``sudo xcode-select -switch /Library/Developer/CommandLineTools` in Terminal.
(This changes the directory for CLT)


2) I copied the ``install_name_tool`` in ``/Library/Developer/CommandLineTools/usr/bin`` and **paste** it in ``/usr/bin`` replacing the ***old and existing*** ``install_name_tool``


3) I deleted rvm, deleted brew


4) Restart.


5) I re-installed brew, ran ``brew doctor`` fixed some of the outputs to get the message ``Your system is ready to brew.``


6) Reinstalled rvm with auto-dotfiles ``curl -L https://get.rvm.io | bash -s stable --auto-dotfiles``


7) Ran ``rvm requirements`` Everything is working perfectly now. 


___

Feel free to [email me](cusxio@gmail.com) if you need a hand !


