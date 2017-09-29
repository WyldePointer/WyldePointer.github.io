---
layout: post
title: "Return of the function"
category: c-language-tutorials
date: 2017-09-05 20:30:11 +0430
tags: [programming,unix,language,pointer,function,int,return,printf]
---

```c_cpp
#include <stdio.h>

int multiply(int base_number, int multiply_by){
  return base_number * multiply_by;
}

int main(int argc, char *argv[]){

  printf("5x2=%d\n", multiply_by(5, 2));

  return 0;
}
```

What happens here is pretty simple: Your function **return**ed a
 number(an `int`) to the caller(or parent function) which is? `main()` or
 `printf()`?

Well, that's up to you to answer and as an another question, you gotta figure
 out the return type of `printf()`. Does it return anything? If it does, are
 you aware of any piece of code around that checks the return value of it, ever?
 

p.s. Title of this post ain't no coincidence: <a href="www.imdb.com/title/tt0345856/" target="_blank">www.imdb.com/title/tt0345856/<a> 
