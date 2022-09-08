# Annotation_task

This repository provides the following tools:

- The Psytoolkit experiment set up (including code and all stimuli)
- Raw data collected from study participants
- Analysis codes with R for the experiment


## Task design

The Annotation_task evaluates the impact of differnt cognitive biases in image annotation (Ambiguity Effect, Bandwagon Effect and Decoy Effect). The current implementation included three levels for the images:

- Level 1 images emphasized lower-level object features
- Level 2 stimuli were chosen for object labeling and contained easily recognizable objects and animals
- Level 3 set consisted of validated face stimuli showing different emotions.

Stimuli were obtained from ImageNet (Level 1 and 2) and NIMSTIM (Level 3) dataset.

A counterbalancing procedure was used in the present task design. Different image levels were also randomized within each bias condition. Decoy effect was not included in the counter balancing due to its different set-up, by combining consecutive images with labels of different levels.

![](https://mega.nz/file/oDQV0ACC#1yUhXDXLi1Xqf1YlsO_tgbGy72c5vtz91eGbMX6_9Y4)


## Usage ##

### Task implementation

The task is implemented in Psytoolkit (https://www.psytoolkit.org/). To use this task, you'll need to upload the experiment.zip file in your Psytoolkit account. The .zip file contains all the stimuli and the code needed for the full experimental set up. To upload it, you will need to click `Create new experiment` from the `Create` menu from the left of the screen, then use the section `Method 2: From a PsyToolkit experiment file (zip format)`.

### Data preparation and analysis

Currently, this experiment collected data from 50 participants. If you want to re-analyze the data or use the same code for preparing or analysing new data, the following files from the `Analysis` folder provide R code for it:

- `Analysis_R/data_prep.md` – takes the raw data (`Raw_data\*`) and combines it in a data.frame
- `Analysis_R/data_lmer.md` – analyse data using lmer 

## Useful links:

- Youtube tutorial on "How to set up and use a PsyToolkit account": https://www.youtube.com/watch?v=nB0DKzxds8U

## References:

- Deng, J., Dong, W., Socher, R., Li, L.-J., Li, K., & Fei-Fei, L. (2009). ImageNet: A large-scale hierarchical image database. 2009 IEEE Conference on Computer Vision and Pattern Recognition, 248–255. https://doi.org/10.1109/CVPR.2009.5206848

- Eickhoff, C. (2018). Cognitive Biases in Crowdsourcing. Proceedings of the Eleventh ACM International Conference on Web Search and Data Mining, 162–170. https://doi.org/10.1145/3159652.3159654 

- Grimaldi, P., Lau, H., & Basso, M. A. (2015). There are things that we know that we know, and there are things that we do not know we do not know: Confidence in decision-making. Neuroscience & Biobehavioral Reviews, 55, 88–97. https://doi.org/10.1016/j.neubiorev.2015.04.006 

- Hill, B. (2013). Confidence and decision. Games and Economic Behavior, 82, 675–692. https://doi.org/10.1016/j.geb.2013.09.009 

- Kim, J., Gabriel, U., & Gygax, P. (2019). Testing the effectiveness of the Internet-based instrument PsyToolkit: A comparison between web-based (PsyToolkit) and lab-based (E-Prime 3.0) measurements of response choice and response time in a complex psycholinguistic task. PLOS ONE, 14(9), e0221802. https://doi.org/10.1371/journal.pone.0221802

- R Core Team. (2017). R: A language and environment for statistical computing [Manual]. https://www.R-project.org/ 

- Rollwage, M., Loosen, A., Hauser, T. U., Moran, R., Dolan, R. J., & Fleming, S. M. (2020). Confidence drives a neural confirmation bias. Nature Communications, 11(1), 2634. https://doi.org/10.1038/s41467-020-16278-6 

- Stoet, G. (2010). PsyToolkit: A software package for programming psychological experiments using Linux. Behavior Research Methods, 42(4), 1096–1104. https://doi.org/10.3758/BRM.42.4.1096

- Stoet, G. (2017). PsyToolkit: A novel web-based method for running online questionnaires and reaction-time experiments. Teaching of Psychology, 44(1), 24–31. https://doi.org/10.1177/0098628316677643

- Tottenham, N., Tanaka, J. W., Leon, A. C., McCarry, T., Nurse, M., Hare, T. A., Marcus, D. J., Westerlund, A., Casey, B., & Nelson, C. (2009). The NimStim set of facial expressions: Judgments from untrained research participants. Psychiatry Research, 168(3), 242–249. https://doi.org/10.1016/j.psychres.2008.05.006

