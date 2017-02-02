# Design Standard

## Purpose
This purpose of this document is to capture the reasoning behind and best practices for design documents.

## Overview
Designs need to be read because changes are needed. If a software product has no bugs and needs no changes its design does not need to be read.

Designs are read in the process of understanding a program because changes need to be made or what changes should be made needs to be investigated. Secondarily, writing a design early exposes problems early and is sometimes a less expensive way to iterate than moving directly into full prototyping.

Asking someone to work on existing code can be like asking a person to finish someone else's painting. To be most effective, you need that person to both appreciate the artist and internalize their style to the point of it becoming second nature.

## What Designs Should Include

### Why
The design should include the whys. Whys argue to the reader why something should not be changed. A design with whys allows a developer to be confident in each new change to the software because they understand the full consequences of that change.

Consider a developer confronted with a design with no whys. One recourse is to extract or reverse-engineer the whys. This is expensive and stressful. Many developers' may have the impulse to "rewrite it from scratch" which can end up being even more expensive.

Keep in mind the long and winding path that led you to believe your current design is the right choice. Your goal is to lead the reader down this same path, but much faster than it took you to traverse it.

When each facet of the design has to fight for its own existence through whys, other benefits emerge. For user-facing design elements, the whys encourage minimalist designs that zero in on what is truly valuable to the user. For technical design elements, the whys encourages less code leading to greater quality and maintainability.

### What
The design should describe the state of the code as it is *intended* to exist. "Intended" means it's okay for the code to not fully match the design as long as there is a scheduled task or bug report whose completion would bring the implementation up to date with the design. It may be a good idea to be more strict about this on a master or "ready-to-ship" branch.

The tight coupling between the design and code should mean that at any point in the repository history, you can see what design was intended.

## Format

### Terms
Organize the document such that it is meant to be read in order. Define and italicize any terms in the text as they appear.

E.g.:
> __*Azure* Is Microsoft's cloud application platform. All global high score data is stored on a SQL Database in the Azure cloud. . .__

### TBDs
Use TBD (to be determined) to indicate details that need to be filled in. TBDs highlight decisions requiring long term study so that they are not lost and do not hold things up. Unresolved TBDs can often serve as talking points for a design discussion or as prompts for an inspector to write a finding providing an opinion. If there are two possible well-defined design solutions for a given problem, entire paragraphs could be TBD. Use Multiple TBDs for things that can be separate parallel investigations.

E.g.:
> __TBD: Decide which sorting algorithm to use__.
 
> __TBD: Customer x found this confusing, consider an alternative__.

> __TBD: Do we think this approach will be performant enough?__

### Hall of Fame
Raw notes and revision history often contain design information, but they are not designs. They often are too large and lack the context to extract this information quickly. Consider an implementer who needs to know why you didn't choose some design i.e. "why didn't you just choose x?" It can be very expensive to extract this information from raw notes.

This is where the hall of fame comes in. At pivotal moments in your design iterations, you may choose design A over the radically different design B. Instead of deleting design B in your next iteration consider cutting it and pasting a condensed version into the hall of fame, along with a paragraph about why it was not chosen. For a UI design, this can be as simple as a few key images and a single paragraph.

## Rules of Thumb
These are some rules of thumb to help keep designs subjective and clear. All examples paraphrase things that have been encountered in real life.

### Rule of Nature
What is the nature of a thing? *Define*, don't *describe*.

Example:

> __Bad: A flater must be able to inflate and deflate messages...__<br>
__Good: A flater inflates and deflates messages...__

Example:

> __Bad: This layer shall also be designed to indicate...__<br>
__Good: This layer also indicates the interface's connection state.__

### Rule of Opposites
Don't write something if the opposite is nonsensical. Improper opposites often reveal inappropriate subjective commentary. The design should stand on its own merit.

Example:

> __Bad: The flater simply takes...__<br>
__Bad: The flater complicatedly takes...__<br>
__Good: The flater takes...__

Example:
> __Bad: Using appropriate protocols, the node...__<br>
__Bad: Using inappropriate protocols, the node...__<br>
__Good: The node...__
	
### Rule of Uncertainty
If it can or should, will it? 

If it will, when will it?

Example:
> __Bad: The node can provide quarks to upper layers.__<br>
__Good: The node provides quarks to upper layers (upon request).__

## See Also
* [Atwood, Jeff. "The Best Code is No Code At All". 30 May 2007](http://blog.codinghorror.com/the-best-code-is-no-code-at-all/)
