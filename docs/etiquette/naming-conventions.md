---
layout: default
title: Naming Conventions
parent: Etiquette
nav_order: 1
---

### Contents
1. [Overarching Philosophy](#overarching-philosophy)
2. [General Naming Guidance](#general-naming-guidance)
3. [Code](#code)
4. [GitHub](#github)
5. [REDCap](#redcap)
6. [PsychoPy and Pavlovia](#psychopy-and-pavlovia)
7. [EEG](#eeg)
8. [Audio and Video](#audio-and-video)
9. [Intentional Deviations](#intentional-deviations)
10. [Helpful Resources](#helpful-resources)

## Overarching Philosophy

All naming conventions for the NDCLab are designed to be:
* human-friendly (that is, they are descriptive and help us navigate all our projects)
* machine-friendly (that is, they make it easy for us to use automated search methods to find what we want in the shortest time possible)
* philosophically aligned with current conventions in the open science community

### Human-friendly
We spend a lot of time looking at a computer screen. So we should use conventions that make things easier on our eyes. Here are some top guidelines to assist:<br/>
* Get used to using lowercase letters for naming things (with a teensy exception for the occasional camelCase)--this means you never have to wonder what to capitalize because you never capitalize anything!
* Build names out of "chunks," which are separated by an underscore (see below for examples).
* Within a chunk, separate words with a hyphen for easy reading (again, teensy exception for camelCase when space is at a premium).
* Use deliberate repetition to enable efficient searching across projects and over time.

### Machine-friendly
Don't confuse the machines. Recognize how computers order things by default (numerically and alphabetically) and avoid feeding them filename cryptonite. Never use:<br/>
:x: spaces<br/>
:x: accented characters (ñöé, etc.)<br/>
:x: special characters (?!:*+, etc.)<br/>

### Open Science Conventions
Our basic conventions are largely based on established standards in psychology and neuroscience, including [BIDS](https://bids.neuroimaging.io/) and [FAIR](https://www.go-fair.org/fair-principles/) principles. See the helpful resources at the bottom of this page for other useful links.

## General Naming Guidance

### Project Names

Project names should be informative but concise. Words are separated by hyphens. All project names begin with a lowercase letter. Examples:

>social-flanker-eeg-dataset<br/>
>social-flanker-eeg-alpha

In some situations, space may be limited. In such cases, hyphens may be replaced with camelCase. Examples:

>brainBox<br/>
>baseEEG

Dataset projects **always** end with "-dataset":
>social-flanker-eeg-dataset<br/>
>readAloud-valence-dataset<br/>
>putt-putt-dataset

Analysis projects associated with a given dataset share the first portion of their project name.  The very first analysis (that is, the main analysis planned at the time of data collection) is typically denoted "-alpha."  (Rare exceptions are made for the sake of playful language.)
>social-flanker-eeg-alpha<br/>
>readAloud-valence-alpha<br/>
>putt-putt-miss

Spin-off analyses retain the first portion of the project name, but utilize an informative suffix:
>social-flanker-eeg-multicultural<br/>
>readAloud-valence-ddm

Given that future data collection spin-offs of a project are common, yet hard to predict, there is no particular effort made to associate data collection efforts in their nomenclature. For example, readAloud-valence-dataset is, philosophically, a spin-off of rwe-dataset, but this is not reflected in the nomenclature.

Project names are used as top-level folder names on GitHub, REDCap, the HPC, and Google Drive.

### Folder Names

The re-use of top-level folder names across projects and platforms is encouraged to simplify navigation. For instance, on the HPC, all active projects have a "sourcedata/raw" folder used for the storage of incoming data from study participants.

Three main paradigms are employed in establishing folder naming conventions for a particular context; the choice depends upon the particular context and use case:

**simple name**
>sourcedata/<br/>
>code/

**chronological ordering**
>2021-08-13_nsf_buzzell_theta-development/<br/>
>2021-10-05_nimh_buzzell_theta-dev-anxiety/

**logical ordering**
>01_design/<br/>
>02_protocols/<br/>
>03_recruitment/<br/>

If using logical ordering, left pad your numbers with zeros, as in the examples above. Since many computer programs order items starting with the first character, this left-padding ensures that "10" actually comes after "09."

### File Names

No two files should share an identical name. Ever.

File names should be built in "chunks."  Examples of potential chunks:

* date
* project name
* a reflection on the document's unique content (e.g. a particular analysis or write-up)

For example, here are some good file names:
> 2021-06-01_social-context-alpha_prelim-analysis_anxiety<br/>
> 2021-06-30_social-context-alpha_prelim-analysis_exec-function

Alternately, if all files are stored within a space specific to the social-context-alpha project and you don't need to track chronology, you could use:
> 01_anxiety_methods<br/>
> 02_anxiety_analysis<br/>
> 03_anxiety_results

### Container Names

One advantage to using [containers](https://ndclab.github.io/wiki/docs/hpc/containers.html) is that you use a preset, deterministic environment to run your code, so that you can expect the same results from running the same code in the container at different times, but this advantage is moot if you can't keep track of what container you used to run your code.

When building a [container](https://ndclab.github.io/wiki/docs/hpc/containers.html), it's important to give it (and its recipe file) a name that provides information about how it differs from prior or future builds. For this we use a three-part [semantic versioning](https://en.wikipedia.org/wiki/Software_versioning#Semantic_versioning) number Major.Minor.Patch appended to the name of the container (e.g. "python-2.1.0"). When you update an existing container with a new feature or updated environment, you should give the new container a version number that encapsulates its relationship to the previous build.

A "minor" change might be updating the included libraries in the container or removing conflicting libraries for example; while a "major" change might be updating the Python version from Python-3.4 to Python-3.7, for example. Commenting inside the recipe file to explain the changes made to new eyes or to your future self is never a bad idea!

### Dates (YYYY-MM-DD)

Whenever dates are used, the [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) convention is used to avoid any ambiguity.  Examples:

>1905-09-27 ([This paper](https://www.astro.puc.cl/~rparra/tools/PAPERS/e_mc2.pdf) was published on this date.)<br/>
>2020-03-11 (The WHO made an [important statement](https://www.who.int/director-general/speeches/detail/who-director-general-s-opening-remarks-at-the-media-briefing-on-covid-19---11-march-2020) on this date.)

## Code

In general, all lab code should align with the conventions used in [PEP 8](https://www.python.org/dev/peps/pep-0008/#naming-conventions) and [BIDS](https://bids-specification.readthedocs.io/en/stable/02-common-principles.html#file-name-structure). Always use descriptive names that will help others understand your code. Additional information on programming standards is available on the [associated wiki page](https://ndclab.github.io/wiki/docs/etiquette/programming-standards.html).

### Function and Method Names

Wherever possible, functions and methods should be re-used across programs when referring to the same thing. For naming them, `lowercase_with_underscores` is used. Example:
> def round_sum (num_1, num_2):<br/>
> &nbsp;&nbsp;&nbsp;&nbsp;return math.round(num_1+num_2)

In special circumstances where names are too long, `camelCase` can be used.

### Class Names

`UpperCamelCase` is used for class names. Example:
>class ImageSprite

### Constants

`CAPITALIZED_WITH_UNDERSCORES` is used for constants. Example:
>MAX_PARTICIPANTS = 10

### Variable Names

For naming variables, `lowercase_with_underscores` is also used. Example:
> subject_name = "bob"

## GitHub

### Repository Names
Tool repositories should be named identically to the associated project. For example:

> pepper-pipeline

Dataset repositories should include the project name and a "-dataset" marker. For example:

> social-context-dataset<br/>
> putt-putt-dataset

Analysis repositories that rely upon an NDCLab dataset should reference the name of the associated dataset. For example:

> social-context-alpha<br/>
> putt-putt-miss

Analysis repositories that rely upon an external dataset can use a descriptive name. For example:

> adult-pre-post-theta

See detailed [notes above](#general-naming-guidance) about regarding project names.

### Branch Names
By default, repositories have a `main` branch and a `dev` branch. New branches are created from the `dev` branch and are named:

> `dev-[feature]`

For example, if Bob creates a new branch to create stimuli for an experiment, he would call it:

> `dev-stimuli`

If only a single individual is working on development of a given feature, then a single feature branch, as named above, will suffice. However, if multiple individuals are working on the same feature branch, then each individual's work should occur within sub-branches that are created from the `dev-[feature]` branch. For example, if Alice wants to help Bob with the `dev-stimuli` branch, she would create a new branch from `dev-stimuli` and call it:

> `dev-stimuli-alice`

Additionally, when Alice creates her new branch off `dev-stimuli`, Bob should also create a branch off `dev-stimuli` and call it:

> `dev-stimuli-bob`

(Note there are two exceptions to the above branch naming rules. The first is the wiki, which does not have a `dev` branch, and new branches are created directly off `main` according to the convention `[feature]-[yourname]`. The second exception applies to external collaborators, who do not have push access to a given NDCLab repo and therefore must make all contributions following a "fork and pull" model. For such external collaborators, branch naming rules still apply, with the exception that it is not necessary to append the external collaborator's name to the branch that lives, by definition, on the personal repository of the external collaborator.)

### Commit Messages
Git commit messages (specifically, the commit subject line) should be concise, informative, and in the imperative tense. There is no final period.<br/>

:white_check_mark: Correct typo<br/>
:white_check_mark: Add counterbalancing content<br/>
:white_check_mark: Optimize function X<br/>
:x: Fix<br/>
:x: Re-wrote the entire script so now it works right<br/>
:x: added a feature.

When useful, a full explanation should be added after the subject line. Example:

```yml
git commit -m "Add full commit message details" -m "Expanded guidance on commit messages to include full commit messages beyond the commit subject line."
```

![gh_full-commit](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/technical/gh_full-commit.png)

The seven great rules of commit messages make for easy reading [here](https://chris.beams.io/posts/git-commit/).

## REDCap

### Project Names
REDCap houses participant questionnaires for a given study. Due to limitations on modifying REDCap projects once data has been collected, changes to the set of questionnaires (including corrections to any existing questionnaire, addition of a new questionnaire, or deletion of a questionnaire) are handled by creating a new REDCap project. Each REDCap project utilizes the NDCLab project name, but is front-ended by the version information. For example:

> 202201v0_readAloud-valence-dataset<br/>
> 202203v0_social-flanker-dataset

The first six digits indicate the year and month when the REDCap data collection project was launched. The number after the letter "v" indicates the specific release within that month. In most cases, projects with by "v0." However, in the event that a revision to REDCap is made twice within the same month, the first release is "v0" and the second is "v1."

### Instrument Names
Each element within REDCap is an "instrument." These should be named:
>instrument_sX_rX_eX

Where:
* `instrument` is the name of the instrument/survey/questionnaire, limited to 10 characters.
* `sX` is the **session** number to distinguish across different time points of a longitudinal study. Sessions typically occur several weeks to years apart.
* `rX` is the **run** number to distinguish logical groupings of data collection within a particular session. Runs can occur on the same day or can occur several days apart.
* `eX` is the **event** number to distinguish repeated use of the instrument before and after an experimental manipulation within a given run.

In the above, "X" is replaced by a numerical value (1, 2, 3) to indicate the ordering of data collection.  For instance, in a longitudinal study, a pre-task questionnaire to establish the "initial state" of a participant is employed. Each instrument employed is numbered distinctly:

| instrument | collection point |
| --- | :-- |
| initState_s1_r1_e1 | gathered during the initial 2021 session with the participant and as part of the first part of the study |
| initState_s1_r2_e1 | gathered during the initial 2021 session with the participant and as part of the second part of the study, but **before** the experimental manipulation |
| initState_s1_r2_e2 | gathered during the initial 2021 session with the participant and as part of the second part of the study, and **after** the experimental manipulation |
| initState_s2_r1_e1 | gathered during a follow-up session in 2023 with the participant and as part of the first part of that follow-up study |

The characters that comprise the `instrument` part of the instrument name should be a reasonable match to the typical acronym used. The following letters can be appended, without any separator, to classify "sister" versions of the instrument:
* `c` or `ca`: the child (and/or adolescent) variation
* `p`: the parent variation
* `es`: the Spanish version

Because `es` is appended directly to an instrument acronym for the Spanish version, and in order to ensure that responses can be counted across English and Spanish surveys for data monitoring purposes, it is imperative that no English instrument be named in such a way that the name ends in "es."

_Note_: When using a zip file to import an existing instrument to REDCap, the instrument name is displayed as:
>Instrument SX RX EX

This is also an acceptable format as data exported from REDCap automatically converts this to `instrument_sX_rX_eX`.

### Variable Names

#### **Scored Instruments**

Variable names are used in REDCap to identify the responses to specific questions asked of study participants. They are **identical to their associated instrument name**, except that `iX` is added to specify the item number. For example, the first three questions of the `initState` instrument would be named:<br/>
> initState_i1\_s1_r1_e1<br/>
> initState_i2_s1_r1_e1<br/>
> initState_i3_s1_r1_e1

#### **Unscored Instruments**

In relatively rare but important cases, such as instruments that gather demographic data, the use of `i1`, `i2`, `i3` for item numbers will be an impediment to data analysis. For surveys that do not get scored or factored for analysis, a more informative convention should be used:<br/>
> demo_sleep_s1_r1_e1<br/>
> demo_exercise_s1_r1_e1<br/>
> demo_caffeine_s1_r1_e1

#### **Other Considerations in Naming REDCap Variables**

**Formatting/Descriptive Variables**
Some variables may not collect any data. These include descriptive elements (e.g., formatted instructions) and fields created to serve as a scaffold for embedded fields. When a REDCap variable does not collect any data, it does not output to the data export. Therefore, there is no need to maintain the session/run/event information in the variable name.
> demo_instruct {an instruction field}<br/>
> demo_contact_embed {a field containing other embedded fields relating to contact info}<br/>
> selfnowA_i6disp_embed {a field that specifically displays the i6 question}

When a survey with such fields will be used twice within a given run (that is, the survey is _e2), add a "2" immediately at the end:
> demo_contact_embed2

**Sub-Items**
By default, if a question within an instrument will require the output of subvariables (this is typically checkboxes where a respondent can check all that apply), REDCap automatically appends `___X` to the end of the base variable name. For instance:<br/>
> initState_i1\_s1\_r1\_e1\___1<br/>
> initState_i1\_s1\_r1\_e1\___2<br/>
> initState_i1\_s1\_r1\_e1\___3

In other cases, however, an instrument may contain sub-items that REDCap cannot automate. For these questions, the sub-item must be built into the variable name manually:
> initState_i1-sub1_s1_r1_e1<br/>
> initState_i1-sub2_s1_r1_e1<br/>
> initState_i1-sub3_s1_r1_e1

**Overrides**
The clinician version of the LSAS includes a quality assurance measure to track when the clinician is "overriding" the standard scoring mechanism particular to this clinical questionnaire. In order to ensure a clear mapping between each scored item (e.g., `i1`) and any override, the override question is numbered `i1ov`:
> lsascl_i8ov_s1_r1_e1

The "ov" immediately after the item number blocks the instruments scoring script from treating this question as a scorable item. Therefore similar logic should be used in other scenarios that require such a solution.


### Updating Instruments

Whenever an instrument is modified (including correction of errors and re-working of questionnaires based on the natural evolution of the lab's research program), a new instrument is created. This enables the lab to track exactly which version of a questionnaire was given to a specific participant.

#### **Scored Instruments**

Scored instruments are revised by appending "_b" (or "_c", "_d", "_z", "_aa", etc.) to the instrument name and to all variables. This must be done very precisely to ensure that the automatic scoring script continues to function as expected. Example:

> instrument name: adexi_s1_r1_e1 :point_right: adexi_b_s1_r1_e1<br/>
> question 1: adexi_i1_s1_r1_e1 :point_right: adexi_b_i1_s1_r1_e1

#### **Unscored Instruments**

Unscored instrument may either use the revisioning system described above for scored instruments (i.e., "_b"). In some cases, such as the initState and postTask questionnaires, it was envisaged that the lab would build up a repertoire of different versions over time. For these instruments, the letter versioning is built directly into the name:

> instrument name: postTaskA_s1_r1_e1 :point_right: postTaskB_s1_r1_e1<br/>
> question 1: postTaskA_i1_s1_r1_e1 :point_right: postTaskB_i1_s1_r1_e1


### Instrument Scores

Each score that is calculated from an instrument receives two variables: the actual score (`scrd`) and the percentage of associated questions that have been answered (`perc`). For clear (and/or single) total scores:

> adexi_b_scrdTotal>br/>
> adexi_b_percTotal

For scores associated with a particular factor, select a few distinguishing letters:

> adexi_b_scrdInh (inhibition score for the adexi) <br/>
> adexi_b_percInh (percentage complete for the adexi inhibition score)<br/>
> adexi_b_scrdWm (working memory score of the adexi)<br/>
> adexi_b_percWm (percentage complete for the adexi working memore score)


## PsychoPy and Pavlovia

### Folder and Experimental Task Names

The folder and the name of the .psyexp file should be identical:
> ft-flanker-o_s1_r1_e1<br/>
> read-aloud-val-o_s1_r1_e1<br/>
> multi-ef_s1_r1_e1

The sX, rX, and eX information follows the logic indicated in the REDCap section above.

The -o flag indicates that the experiment has been designed for online use, via Pavlovia.

The ft- prefix is a special prefix for the three "FIU Toolbox" tasks (flanker, DCCS, and n-back).

Also, use the same experiment name within the PsychoPy settings (the little gear icon):

[!psychopy-exp-name](https://raw.githubusercontent.com/NDCLab/wiki/main/docs/_assets/study-setup/psychopy-exp-name.png)

## EEG

When EEG data is collected, files should be named: `subject` _ `task` _ `datatype` _ `session/run/event`. For example:
> sub-210001_flanker-v5_eeg_s1_r1_e1<br/>
> sub-170044_all_eeg_s1_r1_e1<br/>

Note that "all" refers to cases in which EEG data is collected continuously for all tasks performed in a given study visit.

The sX, rX, and eX information follows the logic indicated in the REDCap section above.

The task name should match exactly the associated PsychoPy (or other) task.

If digitization has also been performed, the digitization zip file should be named: `subject` _ `task` _ `datatype` _ `session/run/event`. For example:
> sub-210001_flanker-v5_digi_s1_r1_e1<br/>
> sub-170044_all_digi_s1_r1_e1<br/>

Note that "all" refers to cases in which EEG data is collected continuously for all tasks performed in a given study visit.

## Audio and Video

When audio, video, or photo data is collected (including Zoom, Audacity, etc.), files should be named: `subject` _ `task` _ `datatype` _ `session/run/event`.  The two acceptable data types are: audio (or audacity), video (or zoom). For example:
> sub-210001_arrow-alert-v1-1_audio_s1_r1_e1<br/>
> sub-150004_social-interaction_video_s1_r1_e1<br/>
> sub-310033_all_audacity_s1_r1_e1<br/>

Note that 'all" refers to cases in which audio/video data is collected continuously for all tasks performed in a given study visit.

The sX, rX, and eX information follows the logic indicated in the REDCap section above.

The task name should match exactly the associated PsychoPy (or other) task.

## Intentional Deviations
There will be some cases in which a file name must deviate from naming conventions in order to contain additional pertinent information about that particular file, or set of files. For example: a participant completes the practice for the PsychoPy task, but decides to discontinue participation before completing the actual PsychoPy task. That participant's practice file will be saved with additional information at the end of the file name:
> sub-311001_arrow-alert-v1-1_psy_s1_r1_e1_practice-only

In cases where an additional string of text must be appended to the end of a file name to convey pertinent information about that file, the file name leading up to the additional string must follow naming conventions and the additional string must be separated from the session/run/event suffix by an underscore (as shown in the example above). If there are more than one file associated with that particular deviation (i.e., in the case of psychopy and eeg data types), all files should contain the additional string of text relevant to the deviation.

For data monitoring purposes, there are additional steps that must be taken when a file name intentionally deviates from convention in order to ensure the file can still be properly handled by data monitoring scripts. Refer to the section titled "Running Data Monitoring" on the [Data Monitoring page](https://ndclab.github.io/wiki/docs/etiquette/data-monitoring.html) for instructions.

## Helpful Resources
* Awesome [slidedeck](https://speakerdeck.com/jennybc/how-to-name-files) from [Jenny Bryan](https://jennybryan.org/).<br/>
* Another awesome [slidedeck](https://slides.djnavarro.net/project-structure/#1) from [Danielle Navarro](https://djnavarro.net/).
* [Brain Imaging Data Structure (BIDS)](https://bids.neuroimaging.io/) for organizing neuroimaging and behavioral data
* [FAIR Guiding Principles](https://www.go-fair.org/fair-principles/) for scientific data management and stewardship
* Psych-DS [technical specification](https://docs.google.com/document/d/1u8o5jnWk0Iqp_J06PTu5NjBfVsdoPbBhstht6W0fFp0/edit#) for psychological datasets (useful even though the project is not very active)
