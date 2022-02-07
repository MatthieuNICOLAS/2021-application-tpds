# Associate Editor
## Comments to the Author:
Although many issues from reviewers have been addressed, two reviewers point out that comparisons with important related work are still missing.

# Reviewer: 1
## Recommendation: Author Should Prepare A Minor Revision
## Comments:
C1. It may be good to explain why the proposed approach is only compared with LogootSplit at the beginning of Section 7.
C2. It may be good to highlight the need to support the concurrent rename operation instead of avoiding generating concurrent rename operations in [18, 19] at the beginning of Section 5.
C3. Typo: It browses the epoch tree and “delete” every epoch…

# Reviewer: 2
## Recommendation: Author Should Prepare A Minor Revision
## Comments:
The authors have addressed the issues I raised in the first submission, and I think the paper is looking good now. I just have a few editorial tweaks:

C1. I'm not familiar with the notation "7k5", but I guess it is supposed to mean "7,500". Please use the more straightforward notation
C2. "matrice" -> "matrix"
C3. "every nodes" -> "every node"
C4. Table 2: giving 6 significant figures is totally excessive; I suggest keeping all numbers to 3 significant figures
C5. What is "Std"? If standard deviation, "StdDev" would be a more descriptive abbreviation. Not sure if it's really meaningful to include standard deviation if the data does not have a Gaussian distribution, maybe better to leave it out and focus on the percentiles.

# Reviewer: 3
## Recommendation: Author Should Prepare A Major Revision For A Second Review
## Comments:
Most of comments are properly addressed. However, the comment about comparisons to related works that is raised by most reviewers is not.

In my opinion, the research article should provide insights to readers, and comparison (in logical writing as well as empirical evaluations) is an important factor. Usually, we see the authors perform comparison evaluation by building comparative works (in fair and objective manner even if it is costly) to make the quality of their publication better and help readers compare the pros and cons of presented works. As pointed earlier, comparison made only with their own work(LogootSplit) is not enough to convince readers about their contribution (if it is a technical report, that would be more than enough).

C1. It is unfortunate that the authors had a hard time to find the implementation of related works. But I believe that this article will make a great impact to the research community if the comparison works are added.
C2. Also, I suggest that the authors revise the current manuscript to emphasize the difference (i.e., pros and cons) between their and related works to enhance readability.

# Reviewer: 4
## Recommendation: Accept With No Changes
