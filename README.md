# Worldwide NER Dataset Improvements

## Overview
This repository contains the dataset with improvements to the annotations in the English Worldwide Newswire test set (https://github.com/stanfordnlp/en-worldwide-newswire), which was first introduced in `Do "English" Named Entity Recognizers Work Well on Global Englishes?` (Shan et. al., 2023) https://arxiv.org/abs/2404.13465. In `SLENDER: Structured Outputs for SLM-based NER in Low-Resource Englishes` (ACL 2025 Industry Track) by Ren and Teo (2025), we have refined the original dataset with more consistent entity labels in the SLENDER format to support research in low-resource Englishes.

## Key Improvements
The improvements focus on ensuring consistent entity labelling across the test set aligned with the English Worldwide Newswire dataset's label definitions (Shan et al., 2023). These include, and are not limited to:
- Standardisation of religious/deity references (e.g., "Allah" → O)
- Correct classification of event/phenomenon mentions (e.g., "Covid-19" → MISCELLANEOUS) 
- Proper handling of nicknames and references to persons (e.g., "Bibi" → PERSON)
- Consistent labelling of temporal expressions (e.g., "December", "Friday" → DATE)
- Accurate classification of geographical locations (e.g., "Haifa" → LOCATION)

## Examples of Label Improvements

| Text | Original Class Label | Improved Class Label | Rationale |
|------|---------------------|---------------------|-----------|
| Officials said the two started firing from a rooftop but were "quickly eliminated by mujahideen with the help of Allah the almighty". | Allah <br> PERSON | Allah <br> O | "Allah", which is the Arabic word for God, is re-labelled as O (not an entity). This is due to the exclusion of deities from PERSON according to the dataset documentation. |
| Xiaomi's decision to tap Vietnam as its latest production base drew public attention as it followed similar moves by major global smartphone makers to move parts of their supply chain from China to Southeast Asia in search of lower costs and more stable production output during Covid-19. | Covid-19 <br> DATE | Covid-19 <br> MISCELLANEOUS | "Covid-19" in this context refers to the pandemic as an event or phenomenon, therefore falling under MISCELLANEOUS. |
| But it was not so easy for me to manage when I encountered Germans. Antisemitism typified the Germans even in those days, and the toxic hatred of Jews welled up in them already then." | Antisemitism <br> PERSON | Antisemitism <br> O | "Antisemitism" describes a form of prejudice, rather than a name of humans. As it does not fall into any of the other classes, it is re-labelled as O (not an entity). |
| First, Shaked noticeably refrained from mentioning whether she would join a government led by opposition leader Benjamin Netanyahu. She mentioned Netanyahu's name only once in her speech: "The housing crisis and high cost of living are not interested in 'yes Bibi, no Bibi.'" | Bibi <br> O | Bibi <br> PERSON | "Bibi" in this context refers to the nickname of Benjamin Netanyahu, and there is a clear connection between "Netanyahu" and "Bibi" in the same text hence re-labelled as PERSON. |
| Other projects included the Electric Company buildings, Haifa's central train station and the old building in the northern city's Bnei Zion Medical Center. | Haifa <br> MISCELLANEOUS | Haifa <br> LOCATION | "Haifa" in this context refers to the city in Israel, and is therefore re-labelled as LOCATION instead of MISCELLANEOUS. |
| The first democratically-elected President of South Africa, and the country's first Black leader, died in December 2013 at age 95. | December <br> O | December <br> DATE | "December" refers to the month and thus labelled as DATE. |
| On Friday morning, Syrian media said that Israel had hit Damascus, killing three military forces and injuring seven more. | Friday <br> MISCELLANEOUS | Friday <br> DATE | "Friday" refers to the day and thus labelled as DATE. |

## Dataset Format
There are 5 datasets, 1 for each region of the Worldwide test set. Each dataset contains the following columns:
- `text`: Original text
- `old_entities`: Original class labels
- `new_entities`: Improved class labels
- `is_updated`: Indication if there is a change in labels

## Citation
If you use this dataset, please cite both the original Worldwide dataset (Shan et. al., 2023) and our improvements:
```
@inproceedings{ren-teo-2025-slender,
    title = "{SLENDER}: Structured Outputs for {SLM}-based {NER} in Low-Resource Englishes",
    author = "Ren, Nicole and Teo, James",
    editor = "Rehm, Georg and Li, Yunyao",
    booktitle = "Proceedings of the 63rd Annual Meeting of the Association for Computational Linguistics (Volume 6: Industry Track)",
    month = jul,
    year = "2025",
    address = "Vienna, Austria",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2025.acl-industry.59/",
    pages = "836--849",
    ISBN = "979-8-89176-288-6",
    abstract = "Named Entity Recognition (NER) for low-resource variants of English remains challenging, as most NER models are trained on datasets predominantly focused on American or British English. While recent work has shown that proprietary Large Language Models (LLMs) can perform NER effectively in low-resource settings through in-context learning, practical deployment is limited by their high computational costs and privacy concerns. Open-source Small Language Models (SLMs) offer promising alternatives, but the tendency of these Language Models (LM) to hallucinate poses challenges for production use. To address this, we introduce SLENDER, a novel output format for LM-based NER that achieves a three-fold reduction in inference time on average compared to JSON format, which is widely used for structured outputs. Our approach using Gemma-2-9B-it with the SLENDER output format and constrained decoding in zero-shot settings outperforms the en{\_}core{\_}web{\_}trf model from SpaCy, an industry-standard NER tool, in all five regions of the Worldwide test set."
}
```
