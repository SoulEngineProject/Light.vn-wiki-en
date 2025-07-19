---
title: 10. Productivity Tips
description: Tips on How to Boost Productivity
published: true
date: 2025-06-13T01:50:59.606Z
tags: 
editor: markdown
dateCreated: 2025-06-13T01:36:24.676Z
---

## Add linebreaks quickly with `.`

Adding `.` at the start of a scenario line will create a new line.
You can use more than one!
```
It's nice to meet you!
...Hello!
```
Will output as
```txt
It's nice to meet you!


Hello!
```

## Use `|` to group commands

Often times, a command will be prefixed by `~`. This symbolizes the start of a code block.

Once you're in a code block, you can use `.` to indicate a line should happen at the same time of the previous line. (Notice how adding linebreaks to text usees `.` to "continue" as well!)

Because Light.vn utilizes a Live Preview, writing multiple commands in one line can help you quickly prototype effects. To separate commands, use the `|` symbol to indicate the end of one command and start of another.
  
As an example, say you have the following code.
~Example~ ~A~
```
~cg0 logo light_splash_1280.png 0 0 90
.fadein logo 800

```

Consider updating it to the following.
~Example~ ~B~
  
```
~cg0 logo light_splash_1280.png 0 0 90 | .fadein logo 800
```

With `Example A`, if you want to edit the position of the object, you need to
- Edit the line with `cg0`
- Re-place your cursor on `.fadein` to check the results in realtime preview
- Repeat until you've placed things in the right position.

With `Example B`, all you need to do is
- Update the position in the command `cg0`: it displays **immediately** since `.fadein` is also on the same line!

Light.vn's sample uses `Example A` in may places to make it beginner-friendly,  
But the pragmatic recommendation is to use `Example B` when possible! 

![image](https://github.com/user-attachments/assets/bceeb69f-046b-4d0d-96e9-d68acdc3bf48)

## Use `|` to group commands (Part 2)

Button commands like the following
```
~button0 choice_02 30 50 80 jump my_file.txt choice
zoom choice_02 95% | .fadein choice_02 600 a3
~btnText choice_02 font.otf 40 "my text"
```

can be updated to
```
~button0 choice_02 30 50 80 "jump my_file.txt choice" | zoom choice_02 95% | .fadein choice_02 600 a3
~btnText choice_02 font.otf 40 "my text"
```

to leverage the realtime preview advantages mentioned above.  

Many of Light.vn's elements that accept a command can be wrapped in `""` to make it clear what the command is. In this case, `jump my_file.txt choice`.

This also makes it clearer what `|` should mean to the engine!

## Create placeholders & prototypes

```
textureCreateRect btn_prototype.png 300 50 255 0 0
textureCreateRect btn_prototype_touch.png 300 50 0 255 0
textureCreateRect btn_prototype_click.png 300 50 0 0 255

~touchableRes btn_prototype.png btn_prototype_touch.png btn_prototype_click.png
~button test1 100 300 80
~btnText test1 NotoSansCJKjp-Regular.otf 24 "click me"

~button test2 100 400 80
~btnText test2 NotoSansCJKjp-Regular.otf 24 "click me too"
```

`textureCreateRect` creates a rectangle that can be cached and reused, similar to `animation` and `textureCreate`.

- (In this case, it creates images called `Images/btn_prototype.png`, `Images/btn_prototype_touch.png`, etc.)
- As an example, you can stash it in a script somewhere for use with all your initial button prototypes. (Perhaps in a place called `/Scripts/prototypes.txt`!)
- Then, delete them once you've created actual image(s) - giving them the same name will prevent script changes.

![image](https://github.com/user-attachments/assets/63863795-cdc2-4777-8c0e-921762f9a5de)

## Use IDs and wildcards to your advantage
When you create any element in Light.vn, it's given an `id`.
```lua
~button id0 0 0 100 "jump title.txt choice1"
~button id1 0 0 100 "jump title.txt choice2"
~if (money >= 30) button id2 0 0 300 "jump title.txt choice3" 

~zoom id0 0 80% | ~zoom id1 80% | .zoom id1 80% // -- Have buttons enter slightly smaller
~.fadein id0 300 a3 | .fadein id1 300 a3 | .fadein id2 300 a3 | .zoom id0 100% 300 | .zoom id1 100% 300 | .zoom id2 100% 300 //-- Zoom & Fade in the buttons

```
On their own, these `id`s aren't particularly powerful. Fading in each element can also become cumbersome when you have a large amount of buttons or objects.

For users looking for more flexibility and speed, giving each `id` a similar prefix allows us to use wildcards (`.*`) to transform each element similarly.

```lua
~button choicebutton_1 0 0 100 "jump title.txt choice1"
~button choicebutton_2 0 0 100 "jump title.txt choice2"
~if (money >= 30) button choicebutton_3 0 0 300 "jump title.txt choice3" 

~zoom choicebutton_.* 80% // -- All buttons beginning with choicebutton_ set to 80% zoom
~.fadein choicebutton_.* 300 a3 | .zoom choicebutton_.* 100% 300 //-- Animate all buttons!
```