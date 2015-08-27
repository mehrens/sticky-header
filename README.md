# sticky-header
Sticky Header for iPhone that prevents Mobile Safari from refocusing input element to center of screen.

# Background
When a user clicks within an form element, Mobile Safari on iOS (at least iOS 6-8) repositions the viewport to center that form element. This is probably done to ensure that whatever form element the user is in gets moved to a spot on screen that would not be covered when the keyboard pops up.

In most cases, this is fine. However, there are some cases where you don't want this behaivor. For example, on a "position: fixed; top: 0px;" header that is supposed to stay sticky to the top of the screen. In this case, if that header has an input field (such as a sticky search box at the top of your site) Mobile Safari will actually treat the positioning as "position: absolute; top: 0px;", and automatically move the entire window back up to the top of the page (since the element you clicked on has "top: 0px;").  So your page jumps and the user experience is not great.

None of the existing workarounds seem to work on iOS 8, and moving the window back to its original position yourself makes things worse since the page still jumps (now twice):

http://stackoverflow.com/questions/6740253/disable-scrolling-when-changing-focus-form-elements-ipad-web-app

# Solution
This solution takes a different approach. Since the body is repositioned when clicking in an form element, why not make it so the body actually never moves in the first place?  At a high level, this is done by locking the body (with "overflow: hidden;", using a DIV for the main content that will be scrolled (using "overflow: auto; width:100%; height:100%;" on the div), and then a second div for the header that is fixed to the top.  

This DIV can be scrolled as much the user wants, and when the user clicks in the header the body (and scrollable div) won't reposition since it was never moved in the first place.
