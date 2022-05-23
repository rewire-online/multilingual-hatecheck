# Multilingual HateCheck: Functional Tests for Multilingual Hate Speech Detection Models

In this repo, you can find **Multilingual HateCheck** (MHC), a suite of functional tests for hate speech detection models in 10 different languages:
Arabic, Dutch, French, German, Hindi, Italian, Mandarin, Polish, Portuguese and Spanish.

For more details, please refer to our paper about MHC, published at the 2022 Workshop on Online Abuse and Harms (WOAH) at NAACL 2022. If you are using MHC, please cite our work!

If you are looking for the original English HateCheck, you can find the data [here](https://github.com/paul-rottger/hatecheck-data) and the paper [here](https://aclanthology.org/2021.acl-long.4/). 

## Repo Structure
**MHC Final Cases** lists the final MHC test cases for each of the ten languages. These are the cases you want to be using to test your model!
The "ingredients" used to arrive at the final MHC cases are stored in **MHC Ingredients**: case templates, placeholders, generated cases, cases for annotation, annotation guidelines and annotations.

## Format of Test Cases
We are providing separate csv files for each of the 10 languages ("hatecheck_cases_final_{LANGUAGE}.csv"), which contain all test cases along with additional information on each test case.
The csv format mostly matches the [original HateCheck data](https://github.com/paul-rottger/hatecheck-data), with some adjustments for specific languages.

**mhc_case_id**:
The test case ID that is unique to each test case across languages (e.g., "mandarin-1305")

**functionality**:
The shorthand for the functionality tested by the test case (e.g, "target_obj_nh").
The same functionalities are tested in all languages, except for Mandarin and Arabic, where non-Latin script required adapting the tests for spelling variations.

**test_case**:
The test case text.

**label_gold**:
The gold standard label ("hateful" or "non-hateful") of the test case. All test cases within a given functionality have the same gold standard label.

**target_ident**:
Where applicable, the protected group that is targeted or referenced in the test case.
All HateChecks cover seven target groups, but their composition varies across languages.

**ref_case_id**:
For hateful cases, where applicable, the ID of the hateful case which was perturbed to generate this test case.
For non-hateful cases, where applicable, the ID of the hateful case which is contrasted by this test case.

**ref_templ_id**:
The equivalent to ref_case_id, but for template IDs.

**templ_id**
The ID of the template from which the test case was generated.

**case_templ**:
The template from which the test case was generated (where applicable).

**gender_male** and **gender_female**:
For gender-inflected languages (French, Spanish, Portuguese, Hindi, Arabic, Italian, Polish, German), only for cases where gender inflection is relevant, separate entries for gender_male and gender_female replace case_templ.

**label_annotated**: 
A list of labels given by the three annotators who reviewed the test case (e.g., "['hateful', 'hateful', 'hateful']").

**label_annotated_maj**: 
The majority vote of the three annotators (e.g., "hateful"). In some cases this differs from the gold label given by our language experts.

**disagreement_in_case**: 
True if label_annotated_maj does not match label_gold for the entry.

**disagreement_in_template**: 
True if the test case is generated from an IDENT template and there is at least one case with disagreement_in_case generated from the same template. This can be used to exclude entire templates from MHC.


## Definition of Hate Speech
We define hate speech as abuse that is targeted at a protected group or at its members for being a part of that group, matching the definition used in the original HateCheck.
Protected groups are groups based on age, disability, gender identity, race, national or ethnic origins, religion, sex or sexual orientation, which broadly reflects Western legal consensus, particularly the US 1964 Civil Rights Act, the UK's 2010 Equality Act and the EU's Charter of Fundamental Rights.
Based on these definitions, we approach hate speech detection as the binary classification of content as either hateful or non-hateful.

## Intended Use of MHC
MHC is primarily meant to be used as a diagnostic tool.
Good performance on a functional test in MHC only reveals the absence of a particular weakness, rather than necessarily characterising a generalisable model strength.
In other words, models that are optimised specifically to perform well on MHC may be able to report 'good' results by overfitting, but this does not necessarily mean that such models would be effective if deployed in the real world.
MHC therefore complements model evaluation on held-out test sets of real-world hate speech rather than substituting it.