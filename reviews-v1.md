# Reviewer: 1

## Recommendation: Author Should Prepare A Major Revision For A Second Review

## Comments:
### Strong points:
S1. The proposed approach is sound.
S2. The figures help understand the approach.
S3. Section 2 is sufficient to provide background knowledge.

### Weak points:
W1. As shown in the example of Figure 10(b), the effectiveness of the garbage collection for different delivery of the rename operations is diverse. The performance of the garbage collection should be theoretically analyzed.
W2. The related work [18, 19] should be included in the experiments as competitive approaches.
W3. The total time (including standard operations and rename operations) should be demonstrated to understand whether the proposed RLS is more efficient than LogootSplit in a comprehensive way.
W4. The results of Figure 11 indicate that only one renaming bot has the best performance, which seems to make Section 5 unnecessary.

## Detailed comments:
D1. The experiments should evaluate the sensitivity to different frequencies to issue rename operations.
D2. The experimental settings for Figure 12 and Table 1 should be specified, e.g., how many renaming bots and whether garbage collection is used.
D3. For Table 1, what is the percentage of each type of remote rename operations?
D4. Typos:
1. Figs. 2, 4-6, 9: Replace "$h$, $e$, $l$" with "$H$, $E$, $L$".
2. (page, column, line) = (4, left, 14), (4, right, -3), (11, left, -12): their states
3. (4, left, -12), (4, right, -16): their local states
4. (4, right, -12), (7, left, -7): every identifier
5. (6, left, 13), (7, right, -1): every node
6. (8, right, 9): $\varepsilon_0 \varepsilon_{A1} \varepsilon_{A8} < \varepsilon_0 \varepsilon_{B2}$
7. (8, right, 16): $\varepsilon_0 \varepsilon_{A1} < \varepsilon_0 \varepsilon_{B2}$
8. (8, right, -21): every epoch
9. (8, right, -11): Every known epoch thus belongs to


## Additional Questions:
1. Please explain how this manuscript advances this field of research and/or contributes something new to the literature.: This paper addresses the efficiency issue in Sequence CRDTs by introducing a rename operation and proposing RenamableLogootSplit (RLS). Extended from their conference version, RLS can deal with concurrent rename operations and garbage collect unused epochs to reduce the space. The simulation results demonstrate RLS with garbage collection requires less space than LogootSplit. The integration time of standard operations of RLS also takes less time than LogootSplit.

2. Is the manuscript technically sound? Please explain your answer under Public Comments below.: Appears to be - but didn't check completely

1. Which category describes this manuscript?: Research/Technology

2. How relevant is this manuscript to the readers of this periodical? Please explain your rating under Public Comments below.: Very Relevant

1. Are the title, abstract, and keywords appropriate? Please explain under Public Comments below.: Yes

2. Does the manuscript contain sufficient and appropriate references? Please explain under Public Comments below.: References are sufficient and appropriate

3. Does the introduction state the objectives of the manuscript in terms that encourage the reader to read on? Please explain your answer under Public Comments below.: Yes

4. How would you rate the organization of the manuscript? Is it focused? Is the length appropriate for the topic? Please explain under Public Comments below.: Satisfactory

5. Please rate the readability of the manuscript. Explain your rating under Public Comments below.: Easy to read

6. Should the supplemental material be included? (Click on the Supplementary Files icon to view files): Yes, as part of the digital library for this submission if accepted

7. If yes to 6, should it be accepted: As is

8. Would you recommend adding the code/data associated with this paper to help address your concerns and/or strengthen the paper?: No

Please rate the manuscript. Please explain your choice.: Good


# Reviewer: 2

## Recommendation: Author Should Prepare A Minor Revision

## Comments:
The paper addresses an important problem, and it seems to be technically sound. My questions and criticisms are fairly minor points that can hopefully be addressed easily in a revision.

The paper does not explain how remove operations interact with rename operations, especially when a remove operation is concurrent with a rename. If the data structure retained tombstones, this would be easy, but a particular selling point of Logoot is its lack of tombstones, i.e. removed elements can be entirely deleted from the data structure. However, will identifier renaming still work correctly when some elements have been removed? For example, the renaming algorithm relies on retrieving the predecessor of a given ID; what happens if this predecessor has been removed? How does reverting a rename operation work when there are removed elements?

When a node issues a rename operation, it broadcasts its entire state to the other nodes. It seems like this could become quite big. In the evaluation section I would be interested to see the average size of the various types of operation (insert, remove, rename) in addition to the time it takes to execute them.

I assume the former state that is included with a rename operation must contain all elements of the sequence at the time the rename was issued, including any elements that are subsequently deleted. In other words, the rename operations effectively include tombstones. The former state of a rename operation can eventually be garbage-collected, but the conditions for this garbage collection (causal stability) are the same conditions for garbage collection of tombstones in CRDTs that require tombstones. I think the paper should be more honest about the fact that in effect, RenamableLogootSplit is no longer a tombstone-free CRDT. This also raises the question: if we need to retain tombstones anyway, then what is the advantage of using a scheme with variable-length identifiers? Can we not simply use an algorithm with fixed-length identifiers (such as RGA) and perform GC of tombstones in the same way as RLS performs GC of renames?

In §5.3, I did not fully understand how the algorithm distinguishes between an insertion that happened causally after the rename being reverted, and an insertion that was concurrent to the rename. It works by leaving off the first element of the ID and examining the tail of the ID, but I would like you to justify why comparing the tail to identifiers in the parent epoch yields the correct result. Also in §5.3, I found the sentence involving MIN_TUPLE and MAX_TUPLE very confusing; please could you explain this more clearly.

The findIndexOfPred function call in Alg. 1 and the getFirstOffset function call in Alg. 2 are unexplained; please give more detail. For the latter, is it really sufficient to have "id" as its only argument? Doesn't it also need "renamedIds" as argument?

If you are short of space, I think §6 could be condensed. It is currently quite a verbose description of what is essentially a simple tree traversal algorithm.

At the beginning of §2, the comparison of fixed-size and variable-length identifiers concludes that both have the downside of "ever-growing overhead". This does not clearly explain the trade-offs between the two approaches.

***

That's all on the content. Otherwise I just have some suggestions for improving grammar and word choice.

In English, an adverb usually appears before the verb, not after. There are many occurrences of this in the paper: "reduce punctually" should be "punctually reduce" (§1); "aggregate dynamically" should be "dynamically aggregate" (§2.1); "assign logically" should be "logically assign" (§2.1); similarly for "impacts negatively" (§2.2); "join and leave dynamically" (§3.1); "applying naively" (§4.2); "be safely" (§6); "impacting negatively" (§7.2); "reducing periodically" (§9.2)

"deepens" (in the abstract) seems like the wrong word. Do you mean "increases"?

"punctually" (occurs twice in §1) seems like the wrong word. Do you mean "periodically"?

§1: "sequence CRDTs exhibits" should be "exhibit"

"we focus on the later approach" should be "latter" (§2)

"cannot" is one word (§2.2 and §8.1)

"unicity" seems like the wrong word; maybe "uniqueness"? (§3.2)

Typo in Alg. 1: "renameIds" should be "renamedIds"

"every" or "each" is followed by a singular noun, e.g. "every identifier" (§4.2), "every node" (§5.2, §6, §7.2), "every epoch" (§6), "each rename operation" (§7.2)

"would no longer depends from" should be "would no longer depend on" (§4.2)

"throught" should be "through" (§5.1)

First sentence of §5.2 should be "To enable every node to select the same target epoch in a coordination-free manner"

"enable to favour" should be "enable favouring" (§5.2); similarly "enable to reduce" should be "enable reducing" (twice in §9.2)

"avoid to rely on" should be "avoid relying on" (§8.1)

"potentiel" should be "potential" (§6)

"performance" should be singular (several times in §7.2 and §8.1)

"several identifier allocation strategy" should be plural (§9.2)

"logged back" (§8.2) seems like the wrong word. Do you mean "backlogged"?

## Additional Questions:
1.  Please explain how this manuscript advances this field of research and/or contributes something new to the literature.: This paper addresses the long-standing problem of metadata growth in CRDTs for collaborative text editing. These algorithms attach a unique identifier to each character of the text, and those identifiers can get quite large, so the size of the identifiers ends up orders of magnitude greater than the content of the text. This paper improves the efficiency of the Logoot/LogootSplit family of algorithms by providing an algorithm for renaming those identifiers to be more compact. It extends the authors' prior work published at PaPoC 2020 by allowing several nodes to concurrently generate rename operations; this is an important extension since it removes the need for coordination.

2. Is the manuscript technically sound? Please explain your answer under Public Comments below.: Yes

1. Which category describes this manuscript?: Research/Technology

2. How relevant is this manuscript to the readers of this periodical? Please explain your rating under Public Comments below.: Very Relevant

1. Are the title, abstract, and keywords appropriate? Please explain under Public Comments below.: Yes

2. Does the manuscript contain sufficient and appropriate references? Please explain under Public Comments below.: References are sufficient and appropriate

3. Does the introduction state the objectives of the manuscript in terms that encourage the reader to read on? Please explain your answer under Public Comments below.: Yes

4. How would you rate the organization of the manuscript? Is it focused? Is the length appropriate for the topic? Please explain under Public Comments below.: Satisfactory

5. Please rate the readability of the manuscript. Explain your rating under Public Comments below.: Easy to read

6. Should the supplemental material be included? (Click on the Supplementary Files icon to view files): Does not apply, no supplementary files included

7. If yes to 6, should it be accepted:

8. Would you recommend adding the code/data associated with this paper to help address your concerns and/or strengthen the paper?: Yes

Please rate the manuscript. Please explain your choice.: Good


# Reviewer: 3

## Recommendation: Author Should Prepare A Major Revision For A Second Review

## Comments:
In this paper, the authors introduced a sequence CRDT belonging to the variable-size identifiers approach, RenamableLogoootSplit. As the authors state (and included to the current submission), the main work of RenamableLogootSplit(RLS) was published before at PaPoc'20. It seems that the major added works (i.e., concurrent rename operation and garbage collection) is non-trivial, however I am not sure whether it is enough to be considered as a separate journal works. Thus, I recommend that the authors add more works to make the current manuscript more suitable to be published as a separate publication, for example empirical performance comparison with the state-of-the-arts.

## Strength:
— Rightly enhancing the previous works

## Weaknesses:
— The size of added works is marginal
— The evaluation is limited and not convincing

## Major comments:
— If the authors provide motivating empirical evaluation results (i.e., numbers) that shows how important the rename operation is, the motivation of this work as well as the contribution of this work become clearer.
— Is there an evaluation for garbage collection?
— It would be better to compare the performance with other works, since currently only LogootSplit is used for the comparison.

## Minor comments:
— Is it necessary to have both 4. RLS without concurrent rename operations and 5. RLS with concurrent rename operations?

## Additional Questions:
1.  Please explain how this manuscript advances this field of research and/or contributes something new to the literature.: The authors propose a new sequence CRDT: RenamableLogootSplit to enhance the performance by renaming without coordination.

2. Is the manuscript technically sound? Please explain your answer under Public Comments below.: Yes

1. Which category describes this manuscript?: Practice / Application / Case Study / Experience Report

2. How relevant is this manuscript to the readers of this periodical? Please explain your rating under Public Comments below.: Relevant

1. Are the title, abstract, and keywords appropriate? Please explain under Public Comments below.: Yes

2. Does the manuscript contain sufficient and appropriate references? Please explain under Public Comments below.: References are sufficient and appropriate

3. Does the introduction state the objectives of the manuscript in terms that encourage the reader to read on? Please explain your answer under Public Comments below.: Could be improved

4. How would you rate the organization of the manuscript? Is it focused? Is the length appropriate for the topic? Please explain under Public Comments below.: Could be improved

5. Please rate the readability of the manuscript. Explain your rating under Public Comments below.: Readable - but requires some effort to understand

6. Should the supplemental material be included? (Click on the Supplementary Files icon to view files): No, it should not be included at all

7. If yes to 6, should it be accepted:

8. Would you recommend adding the code/data associated with this paper to help address your concerns and/or strengthen the paper?: No

Please rate the manuscript. Please explain your choice.: Good


# Reviewer: 4

## Recommendation: Author Should Prepare A Minor Revision

## Comments:
The sequence CRDTs are often used in collaborative online editors, where multiple users conduct local edits and sync with each other periodically. This paper proposes RenamableLogootSplit, which improves their existing study (LogootSplit) using a renaming mechanism. Since LogootSplit's contiguous identifiers do not allow further insertions, more insertions will lead to more identifiers. Renaming will allow us to update the identifiers of all elements, hence effectively reduce the amount of metadata. The evaluation results based on comparing with LogootSplit also suggest less memory consumption and better performance.

The paper is written well. I especially like the way the authors first introduce rename operation and then extend it based on more complicated scenarios, such as concurrent updates and concurrent rename operations. However, the overall paper organization could be improved by introducing more background knowledge at the beginning of the paper to make readers not in this particular field understand the topic sooner. In addition, I also have several technical concerns/questions and hope authors can address them. First, Section 3.2 introduces four properties of rename operations. However, how these properties connect to the proposed renaming mechanism is not clear to me. These properties are not proven as well. Second, the evaluations are purely based on comparing with LogootSplit. It is understandable as the proposed solution is to improve LogootSplit. However, it would be very helpful to include some comparison between RenamableLogootSplit and other state-of-the-art sequence CRDTs. Third, Section 8.1 gives a very good discussion on the difficulties of determining when nodes should issue rename operations. However, these discussions do not lead to a clear strategy for me. Can the authors give guidance on how to use the rename operations in real-world applications?

## Additional Questions:
1.  Please explain how this manuscript advances this field of research and/or contributes something new to the literature.: This manuscript proposes RenamableLogootSplit, an improved version of the authors' pervious LogootSplit work. In this new design, authors introduced renaming mechanism to reassign nodes identifier independently and coordinate later. The experiments show less memory consumption and better performance than LogootSplit.

2. Is the manuscript technically sound? Please explain your answer under Public Comments below.: Appears to be - but didn't check completely

1. Which category describes this manuscript?: Research/Technology

2. How relevant is this manuscript to the readers of this periodical? Please explain your rating under Public Comments below.: Interesting - but not very relevant

1. Are the title, abstract, and keywords appropriate? Please explain under Public Comments below.: Yes

2. Does the manuscript contain sufficient and appropriate references? Please explain under Public Comments below.: References are sufficient and appropriate

3. Does the introduction state the objectives of the manuscript in terms that encourage the reader to read on? Please explain your answer under Public Comments below.: Yes

4. How would you rate the organization of the manuscript? Is it focused? Is the length appropriate for the topic? Please explain under Public Comments below.: Satisfactory

5. Please rate the readability of the manuscript. Explain your rating under Public Comments below.: Difficult to read and understand

6. Should the supplemental material be included? (Click on the Supplementary Files icon to view files): Does not apply, no supplementary files included

7. If yes to 6, should it be accepted:

8. Would you recommend adding the code/data associated with this paper to help address your concerns and/or strengthen the paper?: No

Please rate the manuscript. Please explain your choice.: Good
