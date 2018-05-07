---
layout: page
title: Markdown Stylesheet Demo Thing Also With a Very Long Page Title
permalink: "/theme/"
---

Israh is a responsive Jekyll theme with a clean single column layout and not much else. This theme is an evolution of my [Ezora jekyll theme](https://github.com/ezrasavard/ezora-jekyll-theme) that reflects my own changing tastes. Most notably, Israh takes the focus off of header images so I don't have to find them for posts that don't need them.

Like Ezora, Israh uses a fairly minimal set of layouts and sass, and will automatically conform to a sensible layout based on the YAML provided, unless a layout is specified. Width/height values are all defined in the top of main.scss as variables, so you don't have to hunt too far through the SCSS to tweak things.
Notable includes are the _topbar_, included in the default layout and the _postlist_, which is a paginated pile of posts you can include in any page, like the default home page does. You can specify your navigation menu links in navbar if you don't like it generating them for all your pages, GitHub and LinkedIn accounts. You can also add more social accounts if you like by extending the list in navbar.html.

This page is mostly a copy of [the one from "The Plain" Jekyll Theme](https://github.com/heiswayi/the-plain).

<!--more--->

**NOTE:** This markdown cheatsheet is a typography demo for this theme. Check out this post to learn more about this markdown usage when you want to get started with this theme. Enjoy!

## Typography Elements in One

Let's start with a informative paragraph. **This text is bolded.** But not this one! _How about italic text?_ Cool right? Ok, let's **_combine_** them together. Yeah, that's right! I have code to highlight, so `ThisIsMyCode()`. What a nice! Good people will hyperlink away, so [here we go](#) or [http://www.example.com](http://www.example.com).


<div class="divider"></div>

## Headings H1 to H6

# H1 Heading

## H2 Heading

### H3 Heading

#### H4 Heading

##### H5 Heading

###### H6 Heading

<div class="divider"></div>

## Footnote

Let's say you have text that you want to refer with a footnote, you can do that too! This is an example for the footnote number one [^1]. You can even add more footnotes, with link! [^2]

<div class="divider"></div>

## Blockquote

With some text above it:
> Start by doing what's necessary; then do what's possible; and suddenly you are doing the impossible. --Francis of Assisi

<div class="divider"></div>

## List Items

1. First order list item
2. Second item

* Unordered list can use asterisks
- Or minuses
+ Or pluses

<div class="divider"></div>

## Code Blocks

```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```

```python
s = "Python syntax highlighting"
print s
```

```
No language indicated, so no syntax highlighting.
But let's throw in a <b>tag</b>.
```

Code with line numbers:

{% highlight C  linenos %}
#define PWM16_MAX_VAL 65535
const int led = 2; // the on-board LED pin, configured as output in other code

//configure timer2 for 16 bit PWM usage
void timer_config() {

  NRF_TIMER2-&gt;TASKS_STOP = 1;
  NRF_TIMER2-&gt;MODE = TIMER_MODE_MODE_Timer;
  NRF_TIMER2-&gt;BITMODE = TIMER_BITMODE_BITMODE_16Bit;
  NRF_TIMER2-&gt;PRESCALER = 1; // divide frequency down by 2^x
  NRF_TIMER2-&gt;TASKS_CLEAR = 1; // Clear timer
  NRF_TIMER2-&gt;INTENSET |= TIMER_INTENSET_COMPARE0_Enabled &lt;&lt; TIMER_INTENSET_COMPARE0_Pos;
  NRF_TIMER2-&gt;INTENSET |= TIMER_INTENSET_COMPARE1_Enabled &lt;&lt; TIMER_INTENSET_COMPARE1_Pos;
  NRF_TIMER2-&gt;CC[0] = PWM16_MAX_VAL; // this is related to a bug fix, see "my_isr()" comments
  NRF_TIMER2-&gt;CC[1] = 0;
  NRF_TIMER2-&gt;EVENTS_COMPARE[0] = 0;
  NRF_TIMER2-&gt;EVENTS_COMPARE[1] = 0;
  dynamic_attachInterrupt(TIMER2_IRQn, my_isr);
}
{% endhighlight %}

The ISR:

{% highlight C  linenos %}

void my_isr(void) {

 if (NRF_TIMER2-&gt;EVENTS_COMPARE[0] != 0) {
   NRF_TIMER2-&gt;EVENTS_COMPARE[0] = 0;
   digitalWrite(led, HIGH);
 }
 else if (NRF_TIMER2-&gt;EVENTS_COMPARE[1] != 0) {
   NRF_TIMER2-&gt;EVENTS_COMPARE[1] = 0;
   digitalWrite(led, LOW);
 }
}

{% endhighlight %}

The function to call:

{% highlight C  linenos %}

void pwm16(uint16_t value) {

  NRF_TIMER2-&gt;TASKS_STOP = 1;
  NRF_TIMER2-&gt;EVENTS_COMPARE[0] = 0;
 
  if (value == 0) {
    digitalWrite(led, LOW);
  }
  else if (value == PWM16_MAX_VAL) {
    digitalWrite(led, HIGH);
  }
  else {
    NRF_TIMER2-&gt;CC[0] = PWM16_MAX_VAL - value;
    NRF_TIMER2-&gt;TASKS_START = 1;
  }
}
{% endhighlight %}

## Render some LaTeX with KaTeX

$$
T_{SA} = B_{SA}e^{\frac{E}{k_bT}}
$$

$$
T_{QMC} = B_{QMC}e^{\alpha_D}
$$

$$
T_{QA} = B_{QA}e^{\alpha_D}
$$

<div class="divider"></div>

## Table

### Table 1: With Alignment

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

### Table 2: With Typography Elements

Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3

<div class="divider"></div>

## Horizontal Line

The HTML `<hr>` element is for creating a "thematic break" between paragraph-level elements. In markdown, you can create a `<hr>` with any of the following:

* `___`: three consecutive underscores
* `---`: three consecutive dashes
* `***`: three consecutive asterisks

renders to:

___

---

***

<div class="divider"></div>

## Media

### YouTube Embedded Iframe

<div class="video"><iframe src="https://www.youtube.com/embed/n1a7o44WxNo" frameborder="0" allowfullscreen></iframe></div>

### Image

![Minion](http://octodex.github.com/images/minion.png)

[^1]: Footnote number one yeah baby! Long sentence test of footnote to see how the words are wrapping between each other. Might overflowww!
[^2]: A footnote you can link to - [click here!](#)
