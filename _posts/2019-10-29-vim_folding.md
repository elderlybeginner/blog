---
layout: post
title: Folding markdown in Vim
date: 2019-10-29
tags: [vim, markdown, md, folding]
---

90% of my "pure typing" goes in markdown (thanks to: Gruber and Swartz).  
90% of my "pure typing" goes in Vim (credits to all the crew).  
Thus as the folding idea is brilliant I was fighting to get simple folding in Vim + markdown based on # headers. I felt lack of it, but I was too impatient to implement it or look for it.  
Then on Stack I found what you see below and It made me happy.  
Not perfect, but good enough and works beautifully.

```Vim
function! MarkdownLevel() "folding function
    if getline(v:lnum) =~ '^# .*$'
        return ">1"
    endif
    if getline(v:lnum) =~ '^## .*$'
        return ">2"
    endif
    if getline(v:lnum) =~ '^### .*$'
        return ">3"
    endif
    if getline(v:lnum) =~ '^#### .*$'
        return ">4"
    endif
    if getline(v:lnum) =~ '^##### .*$'
        return ">5"
    endif
    if getline(v:lnum) =~ '^###### .*$'
        return ">6"
    endif
    return "=" 
endfunction
au BufEnter *.md setlocal foldexpr=MarkdownLevel()  
au BufEnter *.md setlocal foldmethod=expr
```

Some tips: zo, zc, zr, zm, zj, zk
