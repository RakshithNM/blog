---
title: Countdown Timer on the Web
date: 2022-09-06
published: true
tags: ['countdown timer', 'side project', 'UX']
canonical_url: false
description: 'Run down of design decisions while building a countdown timer on the web'
---

[TRY COUNTDOWN TIMER](https://countdowntimer-e7e29.web.app/)

I set out to figure out the User Experience behind Countdown Timers and this post is a rundown of all the ideas and thoughts behind the implementation at [COUNTDOWN TIMER](https://countdowntimer-e7e29.web.app/)

# User Experience Implementation Ideas
1. Users should be able to set the time using the provided number keypad.
2. Users should be able to see the set digits.
3. Users should be able to clear(using the “x” button) the set digits.
4. Users should be able to START the timers once they have decided the time is set.
5. Users should not be able to START the timers when all zeros are entered or no time is entered.
6. When users press the START button in the time input screen, users should see the timer active screen.
7. After users press the START button in the time input screen, the timers should start running.
8. When timers are running, users should be able to RESET the running timers to its initial time using the RESET button and PAUSE the running timers using the PAUSE button.
9. When users press the RESET button, the timers should reset to the initial time.
10. When users press the PAUSE button, the timers come to a halt and maintain the progress to how much they have come down to.
11. When timers are reset, users should be able to START(restart) or DELETE the
running timers.(show two buttons - START(restart) and DELETE
12. When users press the START(restart - shown when timers are reset) the timers should start counting down
13. When timers are paused, users should be able to RESUME or DELETE the running timers.(show two buttons - RESUME and DELETE)
14. When timers are restarted(using the START button in the timers running screen), users should be able to PAUSE and RESET the timers.(show two buttons - PAUSE and RESET) - similar to how it behaves when the timer is first started.
15. When users press the RESUME button, the timers should start counting time from the time it was paused.
16. When timers are resumed, users should be able to PAUSE and RESET the timers.(show two buttons - PAUSE and RESET).
17. When users press the DELETE button(only possible when timers are reset), users should be able to set a new time.(take back to time input screen)
18. Once timers are done running, users should be able to set a new time.(show one button - DONE)
19. When the users presses DONE button, users should be able to set a new time.(take back to time input screen)

The points listed above come across as confusing when we read it, but the implementation is much more intuitive.

# Notes On Time Setting
- Users can set time between 00h:00m:00s and 99h:99m:99s
- When the set time is 00h:00m:00s or only zeros are entered users cannot start
the timer.
- We want to users to enter time using any digits not just in the range of 0 to 60 i.e (example 00h:00m:88s - will be considered as 00h:01m:28s, example 00h:65m:10s - will be considered 01h:05m:10s) and start the timer.
- When time above 60 is set for any unit(hours, minutes or seconds) the modulo of the unit is set for it and the next greater unit is incremented. This calculation is done starting from seconds.(examples below).
    > - 00h:00m:88s -> 00h:01m:28s
    > - 00h:59m:99s -> 01h:00m:39s
    > - 02h:59m:60s -> 03h:00m:00s
    > - 99h:99m:99s -> 100h:40m:39s
- Users can enter two zeros at a time.
- The “X”(delete) button is disabled when no time is set.
- The “X” is enabled when at least one digit is set for time.
- The number keys are disabled when all digits are filled.
- The “00”(double zero) button is disabled when the number of digits filled is 5 or greater.

> The time entry is designed to reduce cognitive load on the users and the implementation does not prevent users from entering time within 60 seconds or 60 minutes. Imagine having to count down from 80s and if the restriction is in place, then the user will have to do the conversion mentally(1m 20s) and then enter it.

## The count down timer is working really well and I am spent my time quota on it for now. But I have identified few improvements that we can make to the implementation to make it even better.

1. Provide a preset times the timer can be set to(may be a dropdown component, that lets you pick different duration the timer can be run for - this should ideally be shown in the time input field.
2. Provide a way to set the time individually for hours, minutes and seconds i.e make the hours, minutes and seconds display an input field that can take in user
input.
   > a. This will let users use the virtual keyboard on devices that have them to set hours, minutes and seconds individually.
3. Provide a way to clear the entire set time at once.
   > a. This will let users clear the input field and set a different time when more than one digit is entered.
   > b. Potentially clear the input fields on long press of the “X” button.
4. Provide a way for users to run the timers for more time(example +1m) on the timer running screen.
   > a. For example if the timer is running down and is at 3s, we should be able to make it run from 1m:03s(+1m).
5. Add audio feedback when the timers have completely run down.
6. Let the user know why they cannot start the timer for example when all zeros are entered.
7. Allow users the option to decide against having haptic feedback, it should be a setting.
8. Analog counting down is like a clock, so it could be better if the count down happens anti clockwise.

# Tools used
- [VueCLI](https://cli.vuejs.org/) for project scaffolding
> compiling, linting, serving and building support.
> Straight forward way to deploy to Firebase
- [VueJs](https://v2.vuejs.org/) for state management, components, data driven
> Using Vuex felt like overkill - handled by passing in props and emitting events.
> Needed separation of concerns in terms of components.
> Data driven reactivity of VueJs to make logical sense of UI.
- [Tiny-timer](https://www.npmjs.com/package/tiny-timer) to drive the timers
> Built-in methods, events, properties for all our required user flows.
- [Open Props](https://open-props.style/) to style the UI
> Leads to good design since there is no reference.
> Helps in building a consistent UI.
- SVG for analog clock
> Easy to manipulate using Javascript and CSS
