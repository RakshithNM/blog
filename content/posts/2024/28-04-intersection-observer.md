---
title: Text reveal effect
date: 2024-04-28
published: true
tags: ['Intersection observer']
description: "Run down of how I built text reveal effect"
---

[Cred](https://cred.club) has a pretty cool text reveal effect. I built
a similar effect on the [Bellare grants](https://bellaregrants.netlify.app) website.

I am not exactly sure how the effect on Cred's website was built but the one on
our website is built using the help of intersection observers.

To learn more about Intersection observers, read [here](https://wesbos.com/javascript/06-serious-practice-exercises/scroll-events-and-intersection-observer)

![Text reveal effect](/images/posts/intersection_observer/thumb.png)

```js
const animateTextReveal = (element) => {
  const observerOptions = {
    "threshold": 1
  }
  const observer2Callback = (entries) => {
    entries.forEach((entry) => {
      if(entry.isIntersecting) {
        element.style.color = "white";
      }
      else {
        element.style.color = "gray";
      }
    });
  }
  let observer2 = new IntersectionObserver(observer2Callback, observerOptions);
  observer2.observe(element);
};

const textReveal = () => {
  const yearlyContribDOM = document.getElementsByClassName('yearly-contrib');
  for(const parent of yearlyContribDOM) {
    const yearlyContribPoints = parent.children;
    for(const point of yearlyContribPoints) {
      animateTextReveal(point);
    }
  }
};

textReveal();
```

```css
.yearly-contrib > li {
  transition: color 0.2s ease-in;
}
```

Basically with intersection observers we can do something when an element is
hidden, partially visible or completely visible. We take that to our advantage
and initially keep the text gray and once it is visible make it white, with
a slight transition to smoothen the effect.
