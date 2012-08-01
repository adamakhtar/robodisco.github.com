---
layout: post
title: "CSS - How to mix fixed height elements with an expanding element"
date: 2012-07-16 01:07
comments: true
categories: 
published: false
---

You want to create a page which comprises of a header and footer of fixed height in pixels and then inbetween some content which will expand to fill the remaining screen space now and any time the user resizes the browswer.

Sounds easy, just set the header and footers to height: 26px and the content-holder to 100%.

Wrong! Let's assume the browser's body is currently 900px high.

Setting content-holder to 100% height means 100% height of it's parent, body in this case, so content-holder is equal to 900px. Add the header and footer heights and the total expands beyond the body height and so the footer will be pushed out of sight. 

Attempt 2 Take the header and footers height into account when setting the height's percentage.

Fail! You cant set content-holder's height to 100% - 50px. That's just not possible in CSS.

Soloution 

Absolutely position the 3 elements. 

```css
#header {
  position: absolute;
  top:0px;
  height: 25px;
}

#footer {
  position: absolute;
  bottom: 0px;
  height: 25px;
}

#content-holder {
  position: absolute;
  top: 25px;
  bottom: 25px;
  overflow-y: auto;
}
```
a

