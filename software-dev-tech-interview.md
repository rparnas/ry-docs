# Software Developer Technical Interview

## Purpose
Define a technical interview format for Software developers.

This format has been used as a second-round technical interview. It contains two exercises, a code exercise and a roleplay exercise, aiming at about 30–45 minutes for each.

The availability of AI (whether an interview permits its use or not) was the motivation for the development of the roleplay exercise. In the roleplay, information is revealed incrementally through conversation. Progress depends on a series of small decisions about what to investigate next rather than solving a fixed problem from a complete prompt.

The code exercise remains relatively standard though it was modified with some ideas to make it more AI-aware.

## Code Exercise
* A code exercise is presented with a full spec including test inputs and outputs.
* The candidate may not use AI and must screen share their IDE.
* The candidate is informed that they may ask the interviewer any question (or that they should feel comfortable to think in silence if they desire). In practice, most questions have been clarifications about the prompt or discussions of the candidate's intended approach.
* Aim for the code exercise to be about 30 minutes.
* After the candidate runs their solution, spend 15 minutes asking them to speculate on how they would approach specific extensions to the problem like "What if the input also had to support X?"
* The initial code problem demonstrates basic competence while the extension discussion demonstrates engineering judgment. LeetCode Medium problems were used as a starting point and custom extensions were added by the interviewer ahead of time.

## Roleplay Exercise
This roleplay activity evaluates a candidate's software development skills outside of the realm of "one's own code": requirements gathering, design, cross-team coordination, and risk assessment. It is like a mini D&D scenario where the interviewer acts as the game master while the candidate roleplays the conversations a developer should have before development of a feature begins.

* The candidate receives:
  - A description of your actual development process
  - A raw, messy feature request like a customer would write
* The candidate plays the engineer responsible for owning the feature.
* The interviewer plays all other roles across mini-conversations where the candidate drives most questions. Examples of roles include:
  - Customer success or support lead
  - Product design or UX lead
  - Frontend technical lead
  - Backend technical lead
* The desired outputs are
  - A summary of the feature that is concrete enough for implementation to begin but concise enough that stakeholders could quickly review and understand the proposed direction.
  - A list of risks and unresolved questions
  - A list of commitments from others to do part of the work, or to resolve questions

This roleplay is open-ended. Candidates are evaluated not on reaching a specific solution but on how they gather information and identify what information needs to be gathered.

### Comments and tips

* Using features that already exist in your product makes it easy to give answers to the candidate's questions by drawing on what actually happened during the development of the feature.

* This exercise was designed to last about 30–45 minutes with three 10–15 minute stakeholder conversations and 5–10 minutes for the candidate to summarize things at the end. Small features that a past new hire developer was assigned as their first real feature tend to have a scope that works well.

* The interviewer should answer questions from the perspective of the stakeholder being roleplayed and provide definitive answers when that stakeholder would reasonably have them. The goal is not to withhold information, but to faithfully represent the knowledge, priorities, constraints, and plans that stakeholder would bring to a real feature discussion.

* Strong candidates often begin by asking general questions about the product domain, customers, or development process, or by relating aspects of the scenario to their relevant past experience. In general, I do not count this up-front discussion against the time of the exercise because it is simply bringing forward discussion that would otherwise occur elsewhere later in the interview.

* Your process is not likely pure waterfall. If the candidate says something like "Actually, I would prototype aspect X to discover Y before I talk to Z" the interviewer can fast-forward and tell them the results of that exploration, letting the candidate continue from there.

* This exercise has primarily been used with candidates who have roughly 5+ years of experience. If I were adapting it for less experienced candidates, I might try to redirect the discussion explicitly if the candidate gets stuck on discussing low-impact implementation details. For example: "I assume you can determine whether a field should be a string or a float on your own. Everyone on the team is available now. What information do you want to extract now that would make you stuck if people aren't as available later to give it to you?"
