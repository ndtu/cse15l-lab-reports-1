# **WEEK 4 LAB REPORT**

## Example 1 Code Changes

![Image](pic2-1.png)

The original file can be seen in this [link](MarkdownParse.java). Although this code seems to work for a tester file such as one with the contents of below:
```
# Title

[a link!](https://something.com)
[another link!](some-page.html)
```

it seems to break when there are other characters in the file. For example, a .md file with the other following contents:
```
# Title

[a link!](some-page.html)!
[a link!](https://something.com)
```

will trigger errors and an infinite loop to the java code linked above as shown below:

![Image](pic2-2.png)

Let's address this problem. From the previous example, we see that the code fails because of the value of `currentIndex` which is changed on line 19. Because the `currentIndex` charater is not a `[`, the code goes through the while loop infinitely. We want to fix this by having an `if` statement that accounts for this case that there other extraneous characters.

In summary:
* the **bug** was line 19 which didn't consider the fact to alter the `currentIndex` even if the characters were not found
* the **symptom** was an infinite loop which caused an out of memory error
* the **failure-inducing input** was any characters not part of the links
<br>
<br>
<br>


## Example 2 Code Changes

![Image](pic2-3.png)

The original file can be seen in this [link](MarkdownParseChange.java). Although this code seems to work for a tester file such as one with the contents of below:
```
# Title

[a link!](https://something.com)!
[another link!](some-page.html)abc
```

it seems to break when there are image links to the file. For example, a .md file with the other following contents:

```
# Title

[a link!](some-page.html)!
Hi
![Image](https://chiefrivernursery.com/media/catalog/product/cache/9820170e8aaf17063e79ec8448f2da6f/g/a/gala-apple-fruit_1.jpg)
[a link!](https://something.com)
```

will trigger errors and an infinite loop to the java code linked above as shown below:

![Image](pic2-4.png)

The error is on line 15, the case in the `if` statement that says the character before the brackets is not an `!`. It is causing the program to run an infinite loop while being stuck on the same `currentIndex`. This is causing the program to crash. The simple fix was to make an extra `else` statement that took out the image links.

In summary:
* the **bug** was line 15 which didn't consider the possibility of images
* the **symptom** was an infinite loop which caused an out of memory error
* the **failure-inducing input** was any links to images
<br>
<br>
<br>

## Example 3 Code Changes
