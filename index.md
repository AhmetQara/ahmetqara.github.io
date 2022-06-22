title: "My Blog"
author: "Ahmet Kara"
description: "Welcome to My Blog!" 

# Email / Social media user names used by the minima theme:
# All of these are optional and can be removed or commented out
email: "ahmetkarajob@mail.com"
github_username: "AhmetQara"
linkedin_username: "ahmet-kara-8a64211a6"


#########################################################################################
######### Nothing below needs to be changed (unless you know what you're doing) #########
#########################################################################################
theme: jekyll-theme-hacker

rss: rss

kramdown:
  syntax_highlighter_opts:
    disable: true
    
plugins:
  - jekyll-feed
  - jekyll-sitemap

titles_from_headings:
  strip_title: true
  collections: true

defaults:
  - scope:
      path: ""
      type: post
    values:
      tags: Other


# Posts

[The Hacker Methodology](2022/04/11/The-Hacker-Methodology.html)

[Intro to Offensive Security](2022/04/12/Intro-to-Offensive-Security.html)

[Offensive Pentesting](2022/04/12/Offensive-Pentesting.html)

[Metasploit](2022/04/13/Metasploit.html)

[SQL Injection](2022/04/14/SQL-Injection.html)

[SQL Injection 2](2022/04/15/SQL-Injection-2.html)

