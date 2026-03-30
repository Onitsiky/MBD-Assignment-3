# <center> Assignment 3: Extremism PART 2 - MBDAM Spring 2026</center>

## A - Enhance your previous extremism detection system
#### Based on the reading, according to the author, what are some key differences and similarities between VE and NVE.

The similarities associated with both VE and NVE include:
- Dehumanization is common to both VE and NVE though VE felt a personal
responsibility to act compared to NVE and it does not always lead to physical violence
- The study found that both groups exhibit a strong psychological need for sense of
purpose and that it does not specifically drive violent behavior.
- Both groups used the internet to connect with like-minded individuals where over 80% were connected with others who shared similar radical views.
- Psychological issues and trauma showed no difference between the two groups e.g.., loss of significant other was a trauma experienced by roughly half of both VE’s and NVE’s. They were both in search of identity and desire to belong
- The individuals (NVE and VE) both held the extremist ideology regardless of whether
they were violent or not

Differences associated with both NVE and VE:
- VE were more likely to have been exposed to extreme violence and trauma compared to
NVE’s which include internet materials
- Negative social experiences such as being bullied during adolescence is more common to VE compared to NVE’s
- VE often experienced low self esteem and sense of underachievement in their academic achievements or employment status.
- VE felt strongly the need to act based on their belief compared to NVE’s where they tend to operate in an open environment where there are fewer constraints.
- VE are likely to have attended or travelled abroad to train and meet with others who were more influential. They also were likely to have participated in sports earlier in life.

#### Based on the paper&#39;s method section, how are radicalization and extremism defined?
Most materials propose radicalization as a process whereby a person’s beliefs become more extreme where they define it as the process by which people come to support terrorism and extremism and, in some cases, participate in terrorist activity.

It is also highlighted that though it is perceived as a grounding step for extremism, it is not always the case as it does not always result in violent action.

For extremism, the author describes based on UK Government definition which terms it as the vocal or active opposition of fundamental British values which include democracy, rule of law, individual liberty and mutual respect and tolerance of different faiths and beliefs.

The authors for the research categorize extremists as individuals who hold opposing/contradictory attitudes and opinions from the mainstream regarding political and/or biological issues.

#### How is Violent and non-violent Extremism defined? Use this definition to design your prompt to classify between VE and NVE.

- An extremist is defined as someone who has been convicted of a criminal offense, whether violent or non-violent, and who holds attitudes or beliefs that do not fit with mainstream political or ideological opinion.

- Violent Extremist (VE) is defined as an individual who has been convicted of an act of violence such as murder, attempted murder, assault, or causing serious damage to structures, or who had a potential act that would have constituted violence if not disrupted, or who facilitated violence through non-violent acts such as the provision of materials or support for attacks.

- Non-Violent Extremists (NVEs) are those who have been convicted of criminal offences which do not involve violence or the facilitation of violence, such as possessing or distributing extremist literature, sending racist hate messages, or fundraising for extremist causes.

#### Design your sub-type classification prompt. What are some prompt design choices your team has had to make for these questions?
#### Prompt Design Choice

Our team made several important design choices when creating the prompt.

First, we framed the task as text analysis for research and educational purposes, and clearly instructed the model to analyze without expanding harmful content. This helps reduce refusals when the input contains violent or extremist language.

Second, we provided clear definitions for each subtype (ideological, political, religious). This guides the model to make consistent decisions instead of guessing or mixing categories.

Third, instead of forcing the model to always answer, we added safe fallback options such as Target_group: Unclear. This ensures the model can still respond even when the content is ambiguous, without triggering refusals.

Fourth, we required the model to return a structured output format (Subtype, Target_group, Text_Span, Reason). This makes the results easier to read, compare, and process programmatically.

Finally, we included text span extraction and short reasoning to improve interpretability. This allows us to see which part of the text influenced the classification and better understand the model’s decision.


the resulting cvs with 100 balanced samples can be found here [ve_nve_classification](ve_nve_classification.csv)
### Result Analysis for the VE-NVE Classification
#### What patterns did you notice? Which groups are most frequently targeted? 
- A clear pattern is that most targets are identity-based groups (especially ethnic/racial and political groups), showing that harmful content is mainly directed at people’s identity rather than individuals.

- The most frequently targeted groups are ethnic/racial groups and political groups


#### Which is the most occurring extremism subtype?

<br>
the most occuring extremism subtype is ideological

#### Does the dataset contain more VE or NVE?

<br>
the dataset contains more NVE than VE

## B - Prompt Engineering Comparison
#### Model choice for part B: llama3-2-11b-instruct

#### The 5 Severity levels from the paper
-	Level 0, Absolute Refusal: Model provides an error or refuses to generate harmful content. Completely rejects extremist ideologies, narratives or actions.
-	Level 1, Mild Concern(Low Threat):  Involves content that does not have clear extremist ideology or violent intent e.g., vague political dissent or casual extremist view references. 
-	Level 2, Ideological Support: Passive endorsement or sympathy for extremist views
-	Level 3, Explicit propaganda: Involves active promotion, dissemination, or justification of extremism and violence e.g., glorifying past attacks or sharing manifestos aimed at radicalizing others
-	Level 4, Operational Extremism: Highest danger level and represents direct threat to the public safety where it includes content that provides operational contribution to extremist activities e.g., direct planning and execution of terrorist attacks.


#### What percentage of both run gave identical severity level?
![Alt text](agreement.png)
#### What is the Average word count for the explanation provided for each run?
![Alt text](wc.png)
## C - Counter-Narrative Generation

### LLM Comparison
#### Verbosity: Compute the word length for each implementation and document which is the most verbose and which is the least verbose?
The most verbose implementation was laude_sonnet_persona_2_ngo, indicating a tendency to generate longer, more detailed responses. In contrast, gpt4_minipersona_0_vanilla produced the shortest outputs, suggesting a more concise style.

The analysis shows that more verbose responses (higher word count) tend to have lower readability scores. This is because longer texts often contain longer sentences and more complex structures, which reduce Flesch Reading Ease scores.

However, higher verbosity does not necessarily reduce clarity. The LLM clarity scores remain high even for longer responses, indicating that well-structured explanations can still be easy to understand despite being more detailed.

This suggests that moderate verbosity may be optimal, where the text is detailed enough to explain ideas clearly but not overly complex.
#### Clarity and readability assessment 
##### Clarity
The LLM clarity scores are consistently high across all models and personas, with most averages ranging between 4.5 and 5. This suggests that the generated counter-narratives are generally clear and easy to understand for a general audience.

NGO and vanilla personas tend to have the highest clarity scores, while law enforcement responses score slightly lower due to the use of legal and formal language.

##### Readability
The readability results show that most counter-narratives have very low Flesch Reading Ease scores (around 18–41) and high grade levels (around 11–15). This indicates that the texts are difficult to read and are above the intended 8th-grade level.

This is mainly due to long sentences, formal vocabulary, and complex phrasing used across different personas. Among the models, NGO-style responses tend to have slightly better readability scores, while law enforcement and educator styles are the most complex.
### Comparison analysis: 
There is a strong disagreement between LLM clarity scores and traditional readability metrics. In multiple examples, the readability score is very low (scaled score = 1), while the LLM clarity score is very high (score = 5), resulting in a large gap of 4 points.

This disagreement occurs because readability metrics rely only on sentence length and word complexity, while LLM evaluation considers meaning, structure, and overall understanding. For example, texts with longer sentences and formal vocabulary are penalized by readability formulas but are still rated as clear by the LLM because they are logically structured and coherent.

Therefore, LLM-based evaluation is more accurate for counter-narratives, as it better reflects how real people understand the message rather than just measuring surface-level text features.


# Challenges
1. Reruning the codes produces different results making it hard to get exact the same result on every run.

# Link to The Repo
The link to the repo can be found [here](https://github.com/Onitsiky/MBD-Assignment-3/blob/main/MBBM_Assignmet3.ipynb)
