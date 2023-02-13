---
layout: posts
title: The Four C's: Clarity, Concision, Correctness, Compromise
categories: [tech devrel featured]
---

# Guiding principles of developer documentation

The API team has built new access points that exposes a new feature of your app to the outside world, and now it's your turn to document it.

And you start to do so, and get stuck. How do you balance the bare minimum understanding of the feature with full details about edge cases that developers may run into? What happens if your documentation is strictly correct, but ends up taking more lines of English than there are lines of code implementing the feature? Heck, why not just open-source the code so developers can read the ground truth themselves?

It's a core competency of the DevRel team to get this documentation out the door - it is on the critical path to adoption, after all, so it's a high-value activity. As DevRel owns the developer experience in adoption of your API, how do you optimize for the best possible outcome?

As with so many things that involve humans communicating to humans, there is a hefty helping of judgement to be tapped when producing your documentation. And where judgment is involved, a set of guidelines can be really useful in tuning and maintaining consistency for your approach.

Here's how I think about getting the docs shipped.

### The four C's: Clarity, Consision, Correctness, Compromise.

I tend to think of documenting an API in a semi-hierarchical series; when making a judgment call it helps to view the world as belonging to a spectrum of tradeoffs that lean toward higher priorites when possible. Let's define the main targets that we might aim for and explore some examples of how they provide a good tradeoff when facing a task of documenting software in a complex world.

As a prerequisite, let's start with some statistical definitions to be sure we're on the same page when these terms come up in discussion. I'll refer back to the time-honored practice of describing these terms as darts striking a dart board.

Accuracy:
    The mean value of a set of measurements lies near the true value. Darts on a dartboard are accurate when their average position is near the bullseye, even if they may be inprecise and spread widely across the board.

Precision:
    The deviation of a set of measurements is small. Darts on a dartboard are precise when they are tightly clustered around one spot, even if the average position of the cluster deviates away from the bullseye.

Noise:
    Errors induced in a set of measurements from extraneous sources, i.e. variations in your measurements due to phenomena outside of the system you are measuring. Wind in the room when you're throwing the darts will induce noise into the position of the darts. If my experience is anything to go by, blood alcohol level will also increase the noise of the system.


Clarity:
   The conveyance of the most informative parts of a message. Documentation that promotes understanding provides clarity. If you ask someone reading your message to repeat it back in their own words, and their words sound *accurate*, then you have achieved clarity.

Concision:
    The efficiency of clearly conveying a concept. Editing text to reduce its word count while still retaining its clarity is an exercise in maximising concision. Concise documentation is *precise*.

Correctness:
    The accuracy of your documentation in reflecting real system behavior. Noise, and in particular outliers, are minimized.

