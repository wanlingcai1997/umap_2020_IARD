# **Intent Annotation of Recommendation Dialogue (IARD) Dataset**



## Introduction

The IARD dataset is a labeled recommendation dialogue dataset (the raw dialogues are from <a href="https://redialdata.github.io/website/" target='_blank'>ReDial</a> [[1](#ref1)]). This dataset contains 336 multi-turn recommendation dialogues with 4,583 utterances that were annotated with user intents and recommender actions at the utterance level. In the following, we will introduce the dialogue data we have collected and processed, the two taxonomies we have established respectively for user intents and recommender actions, and our IARD dataset (more details can be found in [[2](#ref2)]).

## Recommendation Dialogue Data

The raw recommendation dialogues are from the <a href="https://redialdata.github.io/website/" target='_blank'>ReDial</a> dataset, which is a publicly available dataset centered around movie recommendations according to [[1](#ref1)]. It was collected by a team of researchers working at Polytechnique Montréal, MILA - Quebec AI Institute, Microsoft Research Montréal, HEC Montreal, and Element AI. 

Specifically, the ReDial dataset was collected through an interface where workers (from Amazon Mechanical Turk) were paired to accomplish a movie recommendation task using natural language. For each pair, one worker was given the role "seeker" who was to seek for interested movies, and the other played the role "recommender" who was responsible for giving recommendations to the seeker. Every conversation session involved at least four movies, and at the end both seeker and recommender were asked some reflective questions for each mentioned movie (e.g., *"Was the movie suggested by the recommender?" "Has the seeker seen the movie?" "Did the seeker like the movie suggestion?"*) that can be used to check their responses' consistency. 

We processed the raw dialogue data in ReDial (that contains 11,348 dialogues) by performing the following four steps:

1. We filtered out dialogues that contain less than three dialogue turns (one dialogue turn denotes a consecutive utterance-response pair: Utterance is from seeker and response is from recommender) and less than four different recommended movies.
2. We removed those with inconsistent answers from seekers and recommenders to the post-conversation reflective questions.
3. We then randomly sampled some satisfactory recommendation dialogues (SAT-Dial) where one recommended movie was not liked by the seeker but a subsequent one was accepted by her/him. These dialogues were aimed to capture the seeker's feedback intents about the recommendation when s/he was not satisfied with it, and furthermore the actions taken by the human recommender that helped the seeker to find a satisfactory item later.
4. We also sampled some unsatisfactory recommendation dialogues (unSAT-Dial) by choosing the dialogues that do not contain any recommendations accepted by the seeker. These dialogues can be useful for detecting what kind of interaction may lead to unsuccessful recommendation. 

Finally, we got 253 satisfactory dialogues (SAT-Dial) and 83 unsatisfactory dialogues (unSAT-Dial) (see [Table 1](#table1) with the statistics).

**<a name="table1">Table 1</a>: Statistics of our selected dialogue data (from ReDial)**

|                                    | SAT-Dial (with user-satisfied recommendation) | unSAT-Dial (without user-satisfied recommendation) |
| :--------------------------------- | :-------------------------------------------- | -------------------------------------------------- |
| # Conversations                    | 253                                           | 83                                                 |
| # Human seekers                    | 125 (# utterances: 1,711)                     | 59 (# utterances: 550)                             |
| # Human recommenders               | 151 (# utterances: 1,747)                     | 68 (# utterances: 575)                             |
| \# Recommended movies per dialogue | 4.57                                          | 4.51                                               |
| # Turns per dialogue               | mean=6.58, min=3, max=19                      | mean=6.49, min=3, max=12                           |
| # Words per utterance              | mean=11.29, min=1, max=72                     | mean=10.72, min=1, max=69                          |



## Taxonomies for User Intents and Recommender Actions

We examined the above-selected recommendation dialogues, in order to understand the language interaction between users (seekers) and human recommenders, based on which we have developed two hierarchical taxonomies for user intents and recommender actions respectively, by using a grounded theory approach (see more details in [[2](#ref2)]).

### Taxonomy for User Intents

The established taxonomy for user intents is aimed to classify the types of utterance inputted by recommendation seekers. We have come up with 3 top-level intents (i.e., **Ask for Recommendation**, **Add Details**, and **Give Feedback**), and 15 sub-intents (see [Table 2](#table2)).

**<a name="table2">Table 2</a>: Taxonomy for user intents**

| Intent (Code)              | Description                                                  | Example                                                      |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Ask for Recommendation** |                                                              |                                                              |
| Initial Query (IQU)        | Seeker asks for a recommendation in the first query.         | *"I like comedy do you know of any good ones?"*              |
| Continue (CON)             | Seeker asks for more recommendations in the subsequent query. | *"Do you have any other suggestions?"*                       |
| Reformulate (REF)          | Seeker restates her/his query with or without clarification/further constraints. | *"Maybe I am not being clear. I want something that is in the theater now."* |
| Start Over (STO)           | Seeker starts a new query to ask for recommendations.        | *"Anything that I can watch with my kids under 10."*         |
| **Add Details**            |                                                              |                                                              |
| Provide Preference (PRO)   | Seeker provides specific preference for the item s/he is looking for. | *"I usually enjoy movies with Seth Rogen and Jonah Hill."*   |
| Answer (ANS)               | Seeker answers the question issued by the recommender.       | *"Maybe something with more action." (Q: "What kind of fun movie you look for?")* |
| Ask Opinion (ASK)          | Seeker asks the recommender's personal opinions.             | *"I really like Reese Witherspoon. How about you?"*          |
| **Give Feedback**          |                                                              |                                                              |
| Seen (SEE)                 | Seeker has seen the recommended item before.                 | *"I have seen that one and enjoyed it."*                     |
| Accept (ACC)               | Seeker likes the recommended item.                           | *"Awesome, I will check it out."*                            |
| Reject (REJ)               | Seeker dislikes the recommended item.                        | *"I hated that movie. I did not even crack a smile once."*   |
| Inquire (INQ)              | Seeker wants to know more about the recommended item.        | *"I haven't seen that one yet. What's it about?"*            |
| Critique-Feature (CRI-F)   | Seeker makes critiques on specific features of the current recommendation. | *"That's a bit too scary for me."*                           |
| Critique-Add (CRI-A)       | Seeker adds further constraints on top of the current recommendation. | *"I would like something more recent."*                      |
| Neutral Response (NRE)     | Seeker does not indicate her/his preference for the current recommendation. | *"I have actually never seen that one."*                     |
| Critique-Compare (CRI-C)   | Seeker requests sth similar to the current recommendation in order to compare. | *"Den of Thieves (2018) sounds amazing. Any others like that?"* |
| **Others**                 | Greetings, gratitude expression, or chit-chat utterances.    | *"Sorry about the weird typing."*                            |


### Taxonomy for Recommender Actions

From recommenders' perspective, we have characterized their behavior at 4 top-level actions (i.e., **Request**, **Respond**, **Recommend**, and **Explain**) and 9 sub-actions (see [Table 3](#table3)).

**<a name="table3">Table 3</a>: Taxonomy for recommender actions**


| Action (Code)                | Description                                                  | Example                                                      |
| ---------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Request**                  |                                                              |                                                              |
| Request Information (REQ)    | Recommender requests for the seeker's preference or feedback. | *"What kind of movies do you like?"*                         |
| Clarify Question (CLA)       | Recommender asks a clarifying question for more details.     | *"What kind of animated movie are you thinking of?"*         |
| **Respond**                  |                                                              |                                                              |
| Respond-Feedback (RES)       | Recommender responds to any other feedback from the seeker.  | *"That's my favourite Christmas movie too! " (U: "My absolute favourite!!")* |
| Answer (ANS)                 | Recommender answers the question asked by the seeker.        | *"Steve Martin and John Candy." (Q: "Who is in that?")*      |
| **Recommend**                |                                                              |                                                              |
| Recommend-Show (REC-S)       | Recommender provides recommendation by showing it directly.  | *"The Invitation (2015) is a movie kids like."*              |
| Recommend-Explore (REC-E)    | Recommender provides recommendation by inquiring about the seeker's preference. | *"Have you seen Cult of Chucky (2017) that one as pretty scary."* |
| **Explain**                  |                                                              |                                                              |
| Explain-Introduction (EXP-I) | Recommender explains recommendation with non-personalized introduction. | *"What about Sleepless in Seattle (1993)? Hanks and Ryan?"*  |
| Explain-Preference (EXP-P)   | Recommender explains recommendation based on the seeker's past preference. | *"Will Ferrell is also very good in Elf (2003) if you're in need of another comedy"* |
| Explain-Suggestion (EXP-S)   | Recommender explains recommendation in a suggestive way.     | *"If you like gory then I would suggest The Last House on the Left (2009).*" |
| **Others**                   | Greetings, gratitude expression, or chit-chat utterances.    | *"Have a good night."*                                       |



## IARD Dataset

### Data Annotation

After the two taxonomies were established, we asked two annotators to label all of the selected dialogue data (see [Table 1](#table1)). Concretely, for each seeker utterance or recommender response, the annotator was encouraged to choose all suitable code(s) that s/he thinks can represent the seeker's intent(s) or the recommender's action(s). They first independently labeled 30 random dialogues, and then met to discuss and resolve any disagreements to ensure annotation quality and consistency, before they started to label the remaining dialogues. For all of the labeled dialogues, the average inter-rater agreement scores (Cohen's kappa [[3](#ref3)] across 15 sub-intents and 9 sub-actions are respectively 0.75 (min=0.50, max=0.95) and 0.82 (min=0.50, max=0.96), which indicate satisfactory agreement according to the interrater reliability [[4](#ref4)].

### Download

Please download the IARD dataset from <a href="https://github.com/wanlingcai1997/umap_2020_IARD.git" target='_blank'>github</a>. 

### Data Fields

- **conversation_id**: a unique id for the conversation (consistent with the "conversation id" in the original <a href="https://redialdata.github.io/website/" target='_blank'>ReDial</a> dataset [[1](#ref1)])
- **accepted_recommendation**: an array that contains positions of utterances where the seeker accepted the recommended item(s) suggested by the recommender (if there is no accepted recommendation, it is an empty array.)
- **dialogue_info**: all of the utterances in the current conversation. For each utterance, there is a unique id (i.e, utterance_id) and its associated information (e.g., utterance position, utterance text).
  - **utterance_id**: a unique id for an utterance, e.g., "S1, R2". Note that for seeker utterance, its id starts with 'S'; for recommender response, its id starts with 'R'; and the contained digital number refers to the utterance position in the conversation.
    - **utterance_pos**: the utterance position in the conversation
    - **worker_id**: the id of the worker in AMT (according to the original <a href="https://redialdata.github.io/website/" target='_blank'>ReDial</a> dataset [[1](#ref1)])
    - **role**: the role of the worker (i.e., "recommender" or "seeker")
    - **utterance_text**: the utterance's content
    - **top-level intent/action**:  the top-level intent(s)/action(s) labeled for the current utterance (that can be seeker utterance or recommender response)
    - **sub-intent/action**: the sub-intent(s)/action(s) labeled for the current utterance (that can be seeker utterance or recommender response)

Note:

- For each movie mentioned in the conversation, we include both the **movie_id** and **movie_name** in the **utterance_text** (e.g., "Me too. Another good one is @124485 <Spaceballs (1987)>.").

**Example Data Format**

```
"1057": {
	"accepted_recommendation": [11],
	"dialogue_info": {
		"S1": {...}
		...
		"R6": {
			"utterance_pos": 6,
			"worker_id": 66,
			"role": "recommender",
			"utterance_text": "Me too. Another good one is @124485 <Spaceballs (1987)> ",
			"top-level intent/action": ["Recommend","Explain"],
			"sub-intent/action": ["REC-S","EXP-I"]
		},
		"S7": {
			"utterance_pos": 7,
			"worker_id": 14,
      "role": "seeker",
   		"utterance_text": "I did see that one, but I didn't really like it...I do love 80s movies though",
      "top-level intent/action": ["GiveFeedback"],
      "sub-intent/action": ["REJ","CRI-A"]
		},
		...
	}
}
```



## Citation

If you use IARD dataset for your research work, please cite the following paper:

- Wanling Cai and Li Chen. 2020. Predicting User Intents and Satisfaction with Dialogue-based Conversational Recommendations. In *Proceedings of the 28th ACM Conference on User Modeling, Adaptation and Personalization (UMAP '20)*, July 14-17, 2020.

**Bibtex entry:**

```latex
@inproceedings{IARD,
  author = {Wanling Cai and Li Chen},
  title = {Predicting User Intents and Satisfaction with Dialogue-based Conversational Recommendations},
  booktitle = {Proceedings of the 28th ACM Conference on User Modeling, Adaptation and Personalization}
  series = {UMAP '20},
  year = {2020},
} 
```



## Usage License

The IARD dataset can be used for any research purposes under the following condition:

- The user may not imply any endorsement from the authors of the paper or Hong Kong Baptist University.
- The user must acknowledge the use of the IARD dataset in her/his publications (see above for the citation information).
- The user may redistribute the dataset as long as it is distributed under the same license conditions.
- The user can not use this dataset for any commercial or revenue-bearing purposes, without obtaining permission from the authors of [[2](#ref2)] (i.e., Wanling Cai and Li Chen).

Neither Hong Kong Baptist University nor any of the researchers involved can guarantee the correctness of the data, its suitability for any particular purpose, or the validity of results based on the use of the dataset.

In no event shall Hong Kong Baptist University and its affiliates or employees be liable to you for any damages arising out of the use or inability to use the data (including but not limited to loss of data or data being rendered inaccurately).

If you have any questions, please feel free to send us an email ([cswlcai@comp.hkbu.edu.hk](mailto:cswlcai@comp.hkbu.edu.hk) and [lichen@comp.hkbu.edu.hk](mailto:lichen@comp.hkbu.edu.hk)).



## Acknowledgement

This work was partially supported by Hong Kong Baptist University IRCMS Project (IRCMS/19-20/D05). We also thank Ms. Yangyang Zheng for her assistance in annotating.



## References

<a name="ref1"> [1]</a> Raymond Li, Samira Ebrahimi Kahou, Hannes Schulz, Vincent Michalski, Laurent Charlin, and Chris Pal. 2018. Towards Deep Conversational Recommendations. In *Advances in Neural Information Processing Systems 31 (NIPS '18)*. 9748-9758.

<a name="ref2"> [2]</a> Wanling Cai and Li Chen. 2020. Predicting User Intents and Satisfaction with Dialogue-based Conversational Recommendations. In *Proceedings of the 28th ACM Conference on User Modeling, Adaptation and Personalization (UMAP '20)*, July 14-17, 2020.

<a name="ref3"> [3]</a> Jacob Cohen. 1960. A Coefficient of Agreement for Nominal Scales. *Educational and Psychological Measurement 20*, 1 (1960), 37-46.

<a name="ref4"> [4]</a> Mary L McHugh. 2012. Interrater Reliability: the Kappa Statistic. *Biochemia Medica 22, 3 (2012)*, 276-282.