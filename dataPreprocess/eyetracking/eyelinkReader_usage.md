
After eyelinkReader::read_edf , sometimes get message like

``` found EBLINK  with no SBLINK 6289152  ```
 
[Eyelink Programmer's Guide](https://www.sr-research.com/support/attachment.php?aid=67) tells us that they don't know why that happened.

EBLINK also known as ENDBLINK, blink end event, mark the reappearance of the eye pupil. SBLINK, also known as STARTBLINK, which I think is specific to EyelinkReader

[Eyelink EDF Access API](https://www.sr-research.com/support/attachment.php?aid=304)


["all periods of tracking loss will be classified as blinks by the online parser."](https://www.sr-research.com/support/thread-9038-post-35326.html#pid35326)


A very short definition of each of the variables is available in the “EDF Access C API user manual.pdf”
gaze$fixations$sttime, 
gaze$fixaionts$entime

fixations$
	gstx: “gaze starting points”
	genx: “gaze ending points”
	gavx: “gaze averages”
	hstx: “headref starting point”
	supd_x: “start units-per-degree”

Pastukhov uses gavx for his plots

sttime is defined in that manual but not sttime_rel !

Maybe the blinks are removed from the time series so I can just use x, y. It says when eye cannot be tracked, for example during blinks, “.” is returned. Although Ruben said that before a blink he sees the position start to go haywire, which suggests the blink isn’t being fully filtered out.

What I really want is a fully labelled time series with all variables including current event, not just start event and end event