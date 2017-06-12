# debounce

I'd like to debounce switches within arduino software. Currently, mark the time an interrupt occures, then measure the amount of time that that has passed in the main loop. When I have reached the time threshold, such as 20ms, I then set the internal state to the steady external state of the button.
However, there are some severe limitations to this method:
1. It only works for two buttons, since there are only two interrupts
2. The millis function resets. Even though it is in hte far future, at some point, it will glitch
3. The main loop might call a long subprocess which causes the button state to not be recognized immediately.

This is what I would like to do to correct these shortcomings:
1. Use pin interrupts instead of 0 and 1, so that I can monitor multiple buttons at once.
2. turn on or reset a counter/timer interrupt for the length of time that I will recognize that the buttons are in a steady state.
3. set the internal state when a timer interrupt is received, and turn off the timer interupt.

I think that this would be a much more robust and general solution.

While I'm in the neighborhood... It would be nice to explore the same algorithm, but using a port expander's pinchange interrupt, instead of the built in port. This might even be easier, via interrupt 0 or 1 on the arduino software.
