# Reflection: SeaBubbles Hawaii with Flexbox

## justify-content and align-items

The way I keep these two straight is that justify-content works along the row and align-items works across it. In the header, justify-content: space-between is what pushed the brand to the left edge and the navigation to the right edge, and align-items: center is what lined them up in the middle of the header's height so one was not sitting higher than the other. They sound similar but they never touch the same direction, so if something is in the wrong spot left to right I go to justify-content, and if it is in the wrong spot top to bottom I go to align-items.

## flex-basis versus the final size

flex-basis is only the starting width of a card, not the width it ends up with. At the medium breakpoint I set flex-basis: 40%, which should leave 20% of the row empty after two cards and the gap. The cards do not stay at 40% though, because flex-grow: 1 lets them split that leftover space and stretch to fill the row. So the basis is what the card asks for and the final size is what it gets after grow and shrink are done with it. The same thing happens at the large breakpoint with 20%, where four cards ask for 80% of the row and grow takes up the rest.

## Experiment 1: justify-content values on the header

Any setting with a list of options is something I want to try every option on, so I ran the header through justify-content: space-between, center, and space-evenly. center pulled the brand and the navigation together in the middle of the header, which looked wrong for a site header. space-evenly spread them out but also left empty space on both outside edges, so the brand was floating away from the left side. space-between was the one that put the brand at the edge and the menu at the other edge, so that is what I kept.

## Experiment 2: align-items values on the course cards

I did the same thing with align-items on .course-card, which controls where the action link sits inside the card. flex-end moved every link to the right side of the card, center put them in the middle, and stretch made each link fill the whole width of the card like a big banner. flex-start kept the link at its natural width on the left under the text, which matched the finished page, so I changed it back to flex-start and left it.

## The bug I fixed

My media queries were not doing anything at first. I had the @media (min-width: 768px) block written out, but the rule inside it was not connected to the right tag, so the browser was applying the flex-basis change to something that did not control the cards and the cards stayed stacked one per row no matter how wide I made the window. Once I pointed the rule inside the query at .course-card, the same selector that has flex-basis: 100% in the main stylesheet, the 40% started replacing the 100% at 768 pixels and two cards per row showed up. The lesson for me was that a media query does not fix anything on its own. It only changes a rule that already exists, so the selector inside has to match the one outside.

## The breakpoints

The two breakpoints are 768px and 992px, and the reason they work is that each one is the point where the next card fits. Below 768 the cards are 100% wide and stack in one column, which is the phone layout and the default, so nothing has to be written for it. At 768 there is enough room for two cards at 40% each with the 20 pixel gap between them, so the medium query switches the basis to 40%. At 992 there is enough room for four cards at 20% each with three gaps, so the large query switches the basis to 20%. Because both queries use min-width and the large one comes last in the file, the large one wins when the window is 992 or wider and the medium one is the only one that matches between 768 and 991. Writing the smallest layout first and only adding changes as the window gets wider meant I never had to undo anything, just replace one number at each step.
