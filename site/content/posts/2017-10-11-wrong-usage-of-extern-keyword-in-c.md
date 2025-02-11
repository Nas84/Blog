---
title: 'Compiling & Dangerous : wrong usage of extern keyword in C'
author: Tiphaine
date: 2017-10-11T13:27:23+00:00
featured_image: /wp-content/uploads/2017/10/first_image.png
pyre_show_first_featured_image:
  - no
pyre_portfolio_width_100:
  - default
pyre_image_rollover_icons:
  - default
pyre_post_links_target:
  - no
pyre_related_posts:
  - default
pyre_share_box:
  - default
pyre_post_pagination:
  - default
pyre_author_info:
  - default
pyre_post_meta:
  - default
pyre_post_comments:
  - default
pyre_slider_position:
  - default
pyre_slider_type:
  - no
pyre_avada_rev_styles:
  - default
pyre_display_header:
  - yes
pyre_header_100_width:
  - default
pyre_header_bg_full:
  - no
pyre_header_bg_repeat:
  - repeat
pyre_displayed_menu:
  - default
pyre_display_footer:
  - default
pyre_display_copyright:
  - default
pyre_footer_100_width:
  - default
pyre_sidebar_position:
  - default
pyre_page_bg_layout:
  - default
pyre_page_bg_full:
  - no
pyre_page_bg_repeat:
  - repeat
pyre_wide_page_bg_full:
  - no
pyre_wide_page_bg_repeat:
  - repeat
pyre_page_title:
  - default
pyre_page_title_text:
  - default
pyre_page_title_text_alignment:
  - default
pyre_page_title_100_width:
  - default
pyre_page_title_bar_bg_full:
  - default
pyre_page_title_bg_parallax:
  - default
pyre_page_title_breadcrumbs_search_bar:
  - default
fusion_builder_status:
  - inactive
avada_post_views_count:
  - 10503
sbg_selected_sidebar:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_replacement:
  - 'a:1:{i:0;s:0:"";}'
sbg_selected_sidebar_2:
  - 'a:1:{i:0;s:1:"0";}'
sbg_selected_sidebar_2_replacement:
  - 'a:1:{i:0;s:0:"";}'
categories:
  - DÉVELOPPEMENT

---
# Compiling & Dangerous {#compiling-dangerous}

C is not a strong typed language but it can run some basic checks. Knowing that, C developers are generally careful because debugging type problems is annoying and can be limited with some simple good practices.

Sometimes a bored developer tries something bold, something new. Here we will detail one of these experiments I recently encountered in a legacy project: **what if we use the `extern` keyword without headers?**

It&rsquo;s uncommon but maybe it&rsquo;s not that bad? Let&rsquo;s see&#8230;

## Test program {#test-program}

<div class="figure">
  <img class="aligncenter" src="http://sogilis.com/wp-content/uploads/2017/10/text.md_.1.png" />
</div>

<div class="figure">
  <img class="aligncenter" src="http://sogilis.com/wp-content/uploads/2017/10/text.md_.2.png" />
</div>

We start from here, a simple program printing his version number. `version` is declared in main file and defined in version file.

I ensure that both declaration and definition are of the same type. Anyway, if something is wrong the compiler will at least raise a warning, right?

## I can&rsquo;t C any problem here {#i-cant-c-any-problem-here}

<div class="figure">
  <img class="aligncenter" src="http://sogilis.com/wp-content/uploads/2017/10/text.md_.3.png" />
</div>

<div class="figure">
  <img class="aligncenter" src="http://sogilis.com/wp-content/uploads/2017/10/text.md_.4.png" />
</div>

To test this I modified version to pass version type from `int` to `char`. There is no complaint from compiler and the version number is correct so obsiously my code is not broken [<sup>1</sup>][1]{#fnref1.footnoteRef}

## A charity problem {#a-charity-problem}

<div class="figure">
  <img class="aligncenter" src="http://sogilis.com/wp-content/uploads/2017/10/text.md_.5.png" />
</div>

<div class="figure">
  <img class="aligncenter" src="http://sogilis.com/wp-content/uploads/2017/10/text.md_.6.png" />
</div>

As the previous program is not bugged I can continue my work, let&rsquo;s add a simple `char ET` in version. Wait, what happened with my version number?

The answer is simple: due to type difference main is reading an `int` of 4 bytes but `version` is defined as char so it is a single byte long. In the previous program due to luck the 3 extra bytes were containing zeroes so the problem was not detected. Simply by adding a new variable we modified one of those bytes and so increased the version number by 256.

We have to fix that. A good practice is to hide implementation with a function call, let&rsquo;s try it!

## Is half a good practice still a good practice? {#is-half-a-good-practice-still-a-good-practice}

<div class="figure">
  <img class="aligncenter" src="http://sogilis.com/wp-content/uploads/2017/10/text.md_.7.png" />
</div>

<div class="figure">
  <img class="aligncenter" src="http://sogilis.com/wp-content/uploads/2017/10/text.md_.8.png" />
</div>

Though I refactored with a function exactly like this stackoverflow thread said, I still get a version number that is complete non-sense.

Well there is a tiny problem: I forgot to update the `main` so the extern declaration is still an int. The version number printed here is the address of the `version` function.

<div class="figure">
  <img class="aligncenter" src="http://sogilis.com/wp-content/uploads/2017/10/text.md_.9.png" />
</div>

<div class="figure">
  <img class="aligncenter" src="http://sogilis.com/wp-content/uploads/2017/10/text.md_.10.png" />
</div>

For curiosity&rsquo;s sake let&rsquo;s make the mirror mistake. Here the program is segfaulting because we&rsquo;re calling the function at adress 42. As 42 is near 0 it&rsquo;s in a non valid memory range and OS raised a segfault. With a different value it might call a valid function, possibly doing something really wrong.

## Understanding the problem {#understanding-the-problem}

By using the `extern` mechanism you tell the compiler: I declared something that&rsquo;s defined elsewhere, you will find at link time. It&rsquo;s problematic for type verification as the linker works simply with symbol names and addresses. All type related information is forgotten at this time.

It can be verified by looking at object files:

<pre class="wp-code-highlight prettyprint">victor@sogilis$ sh gcc -c main2.c
victor@sogilis$ sh gcc -c version3.c
victor@sogilis$ readelf -s main2.o version3.o
File: main2.o
Num   :    Value          Size Type    Bind   Vis      Ndx Name
10    : 0000000000000000     0 NOTYPE  GLOBAL DEFAULT  UND version

File: version3.o
Num:    Value          Size Type    Bind   Vis      Ndx Name
7: 0000000000000000     1 OBJECT  GLOBAL DEFAULT    2 version</pre>

We can see that in `main2.o` `version` size is 0 and has `NOTYPE`.

# Fixing the issue {#fixing-the-issue}

What I would consider a fix is any mechanism that allows type mismatch detection. There are several ways to do that.

## Clean fix {#clean-fix}

<div class="figure">
  <img class="aligncenter" src="http://sogilis.com/wp-content/uploads/2017/10/text.md_.11.png" />
</div>

<div class="figure">
  <img class="aligncenter" src="http://sogilis.com/wp-content/uploads/2017/10/text.md_.12.png" />
</div>

This fix is so obvious I&rsquo;m sure it&rsquo;s a reflex for almost every C developer. If a module defines an extern variable then this variable is part of the module public interface and should be declared in the header.

<div class="figure">
  <img class="aligncenter" src="http://sogilis.com/wp-content/uploads/2017/10/text.md_.13.png" />
</div>

<div class="figure">
  <img class="aligncenter" src="http://sogilis.com/wp-content/uploads/2017/10/text.md_.14.png" />
</div>

Important note: sometimes you can encounter some C code where a module does not include its own header. As we can see with this example, the type conflict is not detected.

The reason is simple: a C definition is also a declaration. So `version5.c` contains two declarations: one in the header and one in the C file, while `version6.c` is compiled without header and there is a single declaration.

## The hostile environment fix {#the-hostile-environment-fix}

When you have a code base already corrupted with bad extern usage, you just can&rsquo;t fix it in a instant. First you want to detect if there are type bugs you have not yet detected with your tests.

It&rsquo;s possible thanks to the `-ftlo` option (for link-time optimizer). With this option the compiler adds metadata about the objects and the linker uses them to perform several optimizations. As the metadata contains the object types, the linker also raises a warning if there is a confusion. To quote documentation:

> if LTO encounters objects with C linkage declared with incompatible types in separate translation units to be linked together (undefined behavior according to ISO C99 6.2.7), a non-fatal diagnostic may be issued.

<div class="figure">
  <img class="aligncenter" src="http://sogilis.com/wp-content/uploads/2017/10/text.md_.15.png" />
</div>

## Use an extern tool to detect extern issues, it&rsquo;s logical! {#use-an-extern-tool-to-detect-extern-issues-its-logical}

With a static code analyzer like `splint` you can detect this kind of problem:

<div class="figure">
  <img class="aligncenter" src="http://sogilis.com/wp-content/uploads/2017/10/text.md_.16.png" />
</div>

# Conclusion {#conclusion}

Without this legacy project I would have never explored that far how much damage can be done in this situation. It reminds us, C developers what a dangerous language we&rsquo;re using, and how special and perfect we are to make it work.

Let&rsquo;s leave the final word to a specialist:

> Christ, people. Learn C, instead of just stringing random characters together until it compiles (with warnings). Linus Torvalds

&nbsp;

Victor Lambret

Special thanks to Graham & Haze for their feedbacks

<li id="fn1">
  for the purpose of this article, let&rsquo;s pretend that I&rsquo;m <strong>that</strong> naive<a href="#fnref1">↩</a></fn></footnotes>

 [1]: #fn1