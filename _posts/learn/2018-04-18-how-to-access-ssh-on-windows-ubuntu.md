---
layout: learning
title: how to access ssh on windows ubuntu
date: 2018-04-18 10:05:18 +0800
categories: learning
tags: ssh
keywords: ssh, windows
---

## Abstract:
This article is to discuss how to generate ssh keys from windows ubuntu.

## Situation:
I want to use create ssh keys in windows environment in order to access my github account without username and password.

## Possible soulutions:
The basic methodology I followed to solve this problem is to do some workaround based on the reference listed below. 
Taking github as an example:
* Step one: generate keys using cmd
    ```
    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
    ```
    This will generate the public and private keys.

    Btw, when we do not specify the file directory, we use the default one. So if we need to generate another ssh keys, we could specify the directory in detail like the example before.

    ```
    ssh-keygen -t rsa -C "your_secondemail@email.com" -f ~/.ssh/second-rsa
    ```

* Step two: copy those keys to the ssh directory of the windows using cmd
    ```
    cp ~/.ssh/. -R /mnt/c/Users/yourusername/.ssh/
    ```
* Step three: add public key into github
* Step four: do some tests.
    one way of test if have correctly connected to the github is to use the below cmd
    ```
    ssh -T git@github.com
    ```
* Step five&six:
    Create an config file in ~/.ssh
    add code like:
    ```
    #lyra007 account
    Host github.com-lyra007
            HostName github.com
            User git
            IdentityFile ~/.ssh/github_rsa
    ``` 

    using <mark>ssh-add</mark> to add rsa identities to authentication agent.
    ```
    ssh-add ~/.ssh/github_rsa
    ```
    Then, you could do the step four again to test.

## Reference:
* (SSH key and the »Windows Subsystem for Linux)[https://florianbrinkmann.com/en/3436/ssh-key-and-the-windows-subsystem-for-linux/]

* (Connecting to GitHub with SSH)[https://help.github.com/articles/connecting-to-github-with-ssh/]

* (Coding help documents)[https://coding.net/help/doc/git/ssh-key.html]