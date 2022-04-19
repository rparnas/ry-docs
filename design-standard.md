# Design Standard

## Purpose
This document includes best practices for software design documents, for both user-facing designs and internal technical designs.

## What should designs include

Designs should include the **what** and the **why**. It is important to keep these elements seperate. "What the software is" tends to remain relevant indefinately whereas "why you made the decisions you made" becomes stale over time because past decisions were made under past conditions and past levels of expertise. This seperation can be accomplished informally. In practice this might mean informally keeping the two elements separated by at least paragraph if not by section.

Define **what** the software is. Leave out subjective commentary in favor of providing a clear, easy-to-understand description. Let the reader judge the design on its own merits especially because the conditions may have changed since the design was made. The **what** can describe the software as it is intended to exist even if the implementation doesn't fully match the design. In that case, deficincies can be documented elsewhere such as in an issue tracker, code comment, or scheduled future task.

Describe **why** the design was chosen. Lead the reader down the long and winding path that led you to settle on the current design so that they don't have to tediously re-discover that path on their own. In addition to background information about the software's domain, the **whys** often include arguments as to why the design shouldn't be changed. Include enough historical context to let the reader evaluate whether or not those arguments still make sense.

For example, if you tried the obvious solution first and it did not work, explain that. If you went with a sub-optimal design due to time contstraints include that information, along with a brief description of the optimal design you would have perferred to use.

If you go far in exploring a design for something but eventually end up rejecting it, consider including a short sumary of the rejected design in a **Hall of Fame**. This section is a good place for information about features that no longer exist or for designs that would be cluttered if interspersed in sections about the current live design. Keep the **Hall of Fame** concise. If you're throwing out a five page design, perhaps pare it down to a one page summary. The goal is to educate readers with a curated history of pivotal design decisions. Don't bombard them with a repository of raw notes.

## When should designs be written

Writing your design information down in a design document tests your design in ways that leaving your design information in a raw format, or no format at all, does not. This is because design writing forces you to think about how you would explain and justify your design to persons external to the project, a new team member, or a user. 

For group activities, such as discussions and meetings, it is useful to start the project with at least a very brief sketch of the design in a design document. Group activities tend to generate high-level design decisions and design insights and it is useful to capture them in the design document as you go. Otherwise they tend to accumulate in raw meeting minutes, notes, or in peoples' heads, and can be costly to extract later. Be on the lookout for activities that generate "design". For example, if you attend a meeting that generates a couple pages of minutes or notes, perhaps afterwards you should capture the design information by writing a paragraph or two into the design document.

Solo work often involves fleshing out design to a high level of detail. There can be a question as to whether it is better work through the design through writing first or if doing prototyping and implementation first would be more efficient. One approach is to keep an eye on whichever activity seems easier at the moment. When you encounter a difficulty spike try to "find your way back to easy" and evaluate whether the issue would be better overcome by switching activities.

When you encounter a difficulty, firstly consider if it stems from the **inherent complexity of the problem.** If so, try using design writing to document that complexity as a guide to help keep you from getting lost in the future. Sometimes this means writing down generic information about the domain. Other times it involves things more specific to the software being developed such as discovering and writing down previously unwritten requirements.

Next, consider if a difficulty stems from **a clear gap or flaw in the software's solution to the problem.** If so, try using design writing to fill in or iterate on the current design. After all, if you can't explain the design even to yourself how will you ever implement it? How will users ever understand it?

If the issue doesn't fall under a category suited to working through via design writing consider prototyping instead. Perhaps you have reached a roadblock in undertsanding the problem space that would be better explored through experimentation. Or perhaps the design is clear but it is unclear whether it would actually work. However, if the design you have written isn't holding your hand through the difficulties you encounter during implementation, this can be a sign you haven't though through the design itself far enough yet.

## Format

Organize the document such that it is meant to be read in order.

### TBDs
Use TBD (to be determined) to indicate details that need to be filled in. TBDs attempt to highlight design decisions that haven't been made yet in such a way that other design work can continue without being held up. If A TBD involves multiple well-defined options, include them in the TBD. TBDs can serve as talking points for a design discussion or as prompts for a design reviewer to write a finding providing an opinion.

Examples:

> __TBD: Decide which sorting algorithm to use.__
 
> __TBD: Customer x found this confusing, consider an alternative__.

> __TBD: Do we think this approach will be performant enough?__

## Rules of Thumb
These are rules of thumb for keeping designs subjective and clear. Examples paraphrase real-life design review findings.

### Rule of Nature
What is the nature of a thing? *Defining* is clearer than *describing*.

Example:

> __Bad: A flater must be able to inflate and deflate messages.__<br>
__Good: A flater inflates and deflates messages.__

Example:

> __Bad: This layer shall also be designed to indicate the interface's connection state.__<br>
__Good: This layer also indicates the interface's connection state.__

### Rule of Opposites
If the opposite of a statement doesn't sound right this often indicates that the original statement includes inappropriate subjective commentary. If commentary is truly needed it should be seperated out.

Example:

> __Bad: The flater simply takes...__<br>
__Opposite: The flater complicatedly takes...__<br>
__Good: The flater takes...__

Example:
> __Bad: Using appropriate protocols, the node...__<br>
__Opposite: Using inappropriate protocols, the node...__<br>
__Good: The node...__

Example:
> __Bad: When this happens, the packet is rejected entirely.__<br>
__Opposite: When this happens, the packet is rejected partially.__<br>
__Good: When this happens, the packet is rejected.__
	
### Rule of Uncertainty
If it *can* or *should*, *will it*? 

If it *will*, *when will it*?

Example:
> __Bad: The node can provide quarks to upper layers.__<br>
__Good: The node provides quarks to upper layers (upon request).__
