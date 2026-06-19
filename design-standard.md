# Design Standard

## Purpose
This document includes best practices for software design documents, for both user-facing designs and internal technical designs.

## What should designs include

The purpose of design documentation is not just to document decisions and specifications, but to do so in such a way that facilitates future work.

Designs should include the *what* and the *why*. The *what* describes the software itself and remains relevant until changes are made. The *why* describes the conditions, assumptions, and reasoning that led to the design. Over time, conditions and assumptions change, causing that reasoning to become stale. Since *what* and *why* age at different rates, keep them separate.

When defining *what* the software is, leave out subjective commentary in favor of providing a clear description. Describe the design, don't argue for it. The *what* should describe behavior and structure that can ultimately be expressed in code and validated through testing.

The *what* may describe the software as it is intended to exist even if the implementation is still in progress. Known gaps between the design and the implementation can be documented in an issue or task tracker, or in code comments.

Describe *why* the design was chosen. Your rationale should preserve the reasoning process, not just the final conclusion. Lead the reader down the path that led you to settle on the current design. Include enough context so that a future reader who desires to make changes can evaluate which of your original arguments still make sense and which have become stale.

The structure of the document should make it easy for a future reader to pick up where you left off. It should be easy to see how new knowledge and new assumptions should alter the reasoning and cascade into design changes. For example:

"We first considered Design A. Design A would have been simpler, but it could not satisfy requirement X. Requirement X was considered mandatory because of Y. Therefore we chose Design B."

...might be modified in the future to:

"...Therefore we originally chose Design B. Version 2 of the underlying library satisfies Requirement X (which is still mandatory because of Y). Thus we were able to pivot back to Design A. This fixes the unexpected negative side-effects that Design B caused (including A, B, and C)."

This example can be completed by replacing portions of the *what* section to match the pivot to design A.

Keep your *whys* concise. An hour of discussion should often only generate a sentence or two of design rationale. Do not bombard future readers with a repository of raw notes.

## When should designs be written

A design document can often start out small. Discussions, meetings, and other group activities often generate design decisions early in the life of a feature. Document design information as it comes up. Otherwise it will tend to accumulate in meeting minutes, notes, and people's heads, where it can be costly to extract later.

Design documentation is not just the output of design work. It is a tool for exploring and resolving design problems. The act of explaining and justifying a design in writing helps reveal ambiguities, conflicting assumptions, and unresolved questions. Don't wait until the design is "finished" before writing it down or you will often discover that your design is much less "finished" than you realized.

Design writing and code prototyping can both be exploratory tools, but they are effective at different things. Design writing is often more effective at working through ambiguities, assumptions, and open questions. This is because design writing allows you to work directly in the language of the problem domain. Code prototyping is often more useful for answering questions about whether a solution can be built. Testing a prototype is useful for answering questions about whether that solution actually achieves the desired outcome. When progress stalls, consider whether you are using the wrong tool for the question you are trying to answer.

## Format

Arrange information in order such that later sections build on earlier sections. Often this means putting domain information and important definitions up front before diving into details.

### TBDs
Use TBD (to be determined) to indicate details that need to be filled in. TBDs are a mechanism for recording unresolved design questions without blocking the rest of the document. If A TBD involves multiple well-defined options, write down the options. TBDs can serve as an agenda for a design discussion or prompts for a design reviewer to write their opinion. Don't pretend the design is finished when it isn't.

Examples:

> __TBD: Decide which sorting algorithm to use.__
 
> __TBD: Customer x found this confusing, consider an alternative__.

> __TBD: Do we think this approach will be performant enough?__

## Rules of Thumb
These are rules of thumb for keeping designs objective and clear. Examples paraphrase common real-life design review findings.

### Rule of Nature
What is the nature of a thing? *Defining* is clearer than *describing*. Don't write requirements about the design. Write the design.

Example:

> __Bad: A flater must be able to inflate and deflate messages.__<br>
__Good: A flater inflates and deflates messages.__

Example:

> __Bad: This layer shall also be designed to indicate the interface's connection state.__<br>
__Good: This layer also indicates the interface's connection state.__

### Rule of Opposites
If the opposite of a statement would be nonsensical this often indicates that the original statement is making subjective commentary. Leave out such commentary to make the design easier to read and change.

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
Describe behavior not possibilities.

If it *can* or *should*, *will it*? 

If it *will*, *when will it*?

Example:
> __Bad: The node can provide quarks to upper layers.__<br>
__Good: The node provides quarks to upper layers (upon request).__
