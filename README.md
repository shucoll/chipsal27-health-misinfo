# HealthMisinfo: Shared Task on Health Misinformation Detection at CHiPSAL-IndoNLP 2027

**Competition link:** [Codabench](https://www.codabench.org/competitions/18660/)

**Health misinformation detection in a low-resource language**

Health misinformation spreads quickly on social media. False claims about treatments, vaccines and the causes of disease have been linked to delayed treatment and vaccine hesitancy. Automated detection has mostly been built for English, which leaves speakers of low-resource languages such as Nepali, a language of more than 30 million people, without these protections. The shared task is part of the CHiPSAL-IndoNLP 2027 workshop at COLING 2027, and the competition is hosted on Codabench.

## Task

Given a Nepali health-related post, decide whether it is **misinformation (fake)** or **factual (real)**.

The data comes from **Nep-Health-Misinfo** (Maharjan et al., 2026), the first human-verified Nepali corpus for health misinformation detection. It was built by adapting four English benchmarks, CoAID, COVID-19, Monkeypox-V1 and Monkeypox-V2, through machine translation followed by careful post-editing by native Nepali speakers. The post-editors kept the medical meaning and the deceptive content of each claim intact while making the Nepali read naturally. Hashtags and abbreviations such as WHO and CDC are kept in their original form.

**To learn more about the dataset**, see the [dataset paper](https://aclanthology.org/2026.chipsal-1.20/).

## Participation

Join the competition on Codabench: [HealthMisinfo: Shared Task on Health Misinformation Detection](https://www.codabench.org/competitions/18660/)

The competition has two phases:

* **Development phase:** train on the training data and submit predictions for the eval posts. Scores appear on the leaderboard.
* **Test phase:** submit predictions for the test posts. Your **last** submission in this phase is the one that is ranked.

## Dataset

Every post has a unique identifier, `id`. All files are UTF-8 CSV.

| Data | Files | Posts | Columns | Link |
|------|-------|-------|---------|------|
| Train | `train.csv` | 3,325 | `id`, `text`, `label` | [Link](https://drive.google.com/drive/folders/1jJjcswbdJJhhKjEu0H2SkmwpAWMn92cg?usp=sharing) |
| Eval | `eval.csv`, `sample_submission_eval.csv` | 714 | `id`, `text` | [Link](https://drive.google.com/drive/folders/1QxYhfjAXBwnE-mDA3qM4YAZnD_zyxbXe?usp=sharing) |
| Test | `test.csv`, `sample_submission_test.csv` | 714 | `id`, `text` | Released on Jan 4, 2027 |

`label` is **0 for real** (factual) or **1 for fake** (misinformation). About 41% of the posts are fake. The splits are stratified by source dataset and label, and no text appears in more than one split.

## Use of External Data

External datasets and pretrained models are allowed. Describe any external data you use in your system description paper.

**Not allowed:** the posts are translations of public English datasets (CoAID, COVID-19 and Monkeypox). Do not use the labels from those original datasets to label the eval or test posts.

## Evaluation

Submissions are ranked by **macro F1**: the F1 score is computed separately for the real and fake classes and the two are averaged, so both classes count equally.

```python
from sklearn.metrics import f1_score
f1_macro = f1_score(gold, predicted, average="macro")
```

The leaderboard also shows **accuracy**, **macro precision** and **macro recall**, for information only.

## Submission Format

Your submission file must be a CSV file named `predictions.csv` with the columns `id` and `label`, one row for every post in the current phase (`eval.csv` in the Development phase, `test.csv` in the Test phase). `label` must be `0` (real) or `1` (fake). Zip the file and submit the zip.

| id | label |
|----|-------|
| 1007 | 0 |
| 1008 | 1 |
| 1009 | 0 |

A sample submission for the Development phase is in this repository: [sample_submission.csv](sample_submission.csv). To check your setup, rename it to `predictions.csv`, zip it, and submit it to the Development phase.

If something is wrong with your file (missing ids, ids from the other phase, labels other than 0 or 1, duplicate rows), the submission fails. Click it on Codabench and open the **Scoring errors** tab to see what to fix. Failed submissions don't count toward your limit.

## Publication

Participants in the shared task are expected to submit a system description paper to the CHiPSAL-IndoNLP 2027 workshop at COLING 2027. Submitting a paper is not mandatory to participate in the shared task. Papers must follow the workshop submission instructions and will be peer reviewed. Acceptance depends on the quality of the paper, not on the shared task results. All accepted papers will be published in the COLING 2027 workshop proceedings.

## Registration and Proceedings

The registration fee is not required for publication of accepted shared-task papers in the workshop proceedings. Anyone who wishes to attend the workshop, either in person or virtually, must register in accordance with the main conference’s registration policy.

## Timeline

* Start of the competition (Development phase starts; train and eval data released): Nov 20, 2026
* Test phase starts (test data released): Jan 4, 2027
* Test phase ends: Feb 24, 2027
* Shared task paper submission deadline: Feb 28, 2027
* Notification of acceptance: March 31, 2027
* Camera-ready papers due: April 4, 2027

Phase times are in UTC: the Development phase closes on Jan 3, 2027 at 23:59 and the Test phase on Feb 24, 2027 at 23:59.

## Organizers

* Surendrabikram Thapa (Virginia Tech, USA)
* Shuvam Shiwakoti (Virginia Tech, USA)
* Siddhant Bikram Shah (Northeastern University, USA)
* Kritesh Rauniyar (Macquarie University, Australia)
* Surabhi Adhikari (Columbia University, USA)
* Kristina T. Johnson (Northeastern University, USA)
* Kengatharaiyer Sarveswaran (University of Jaffna, Sri Lanka)
* Bal Krishna Bal (Kathmandu University, Nepal)
* Usman Naseem (Macquarie University, Australia)

## Contact

If there are any questions related to the competition, please contact the organizers at ssiwakoti12@gmail.com. Participants in this shared task are encouraged to reach out with any concerns or questions to any of the shared task organizers.

## References

* Maharjan, S., Shrestha, A., Thapa, L., Poudel, S., Shiwakoti, S., Thapa, R., Rauniyar, K., & Thapa, S. (2026). Improving Public Health Safety in Low-Resource Languages Using a Human-Verified Health Misinformation Corpus and Large Language Models. In *Proceedings of the Second Workshop on Challenges in Processing South Asian Languages (CHiPSAL 2026) @ LREC*, pages 209–218. [ACL Anthology](https://aclanthology.org/2026.chipsal-1.20/)
* Cui, L., & Lee, D. (2020). CoAID: COVID-19 Healthcare Misinformation Dataset. *arXiv:2006.00885*.
* Patwa, P., et al. (2021). Fighting an Infodemic: COVID-19 Fake News Dataset. In *CONSTRAINT 2021 (Combating Online Hostile Posts in Regional Languages during Emergency Situations)*.
* Crone, S. (2022). Monkeypox Misinformation: Twitter Dataset.
