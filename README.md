# TRATES: Trait-Specific Rubric-Assisted Cross-Prompt Essay Scoring (ACL Findings 2025) 
https://aclanthology.org/2025.findings-acl.1054/

**TRATES** is a Trait-specific and Rubric-Assisted cross-prompt AES framework that combines **generic writing-quality features** with **trait-specific features** automatically generated via a large language model (LLM).  Given a trait rubric, TRATES uses an LLM in two stages:
1. **Rubric-based Feature Generation** – The LLM generates a set of questions from the rubric to assess a specific trait.  
2. **Trait-Specific Feature Extraction** – The LLM answers each question individually, given the essay.  
Finally, the extracted trait-specific features are combined with writing-quality and prompt-specific features to train a **cross-prompt regression model** that predicts trait scores for essays from unseen prompts.  

This repository contains all the extracted trait-specific features.  

---

## 📁 Feature File Organization

The feature files in this repository are organized by **dataset**, **trait**, **LLM name**, and (for ASAP) **rubric**.

---

### 📚 ASAP Dataset

The `ASAP/` folder contains feature files for **eight writing traits**:

- `content/`
- `conventions/`
- `language/`
- `narrativity/`
- `organization/`
- `prompt_adherence/`
- `sentence_fluency/`
- `word_choice/`

Each trait folder includes the features extracted by **three LLMs**:

- `gemma-2-9b-it-SimPO/` 🤗 [link](https://huggingface.co/princeton-nlp/gemma-2-9b-it-SimPO)
- `Llama-3.1-8B-Instruct/` 🤗 [link](https://huggingface.co/meta-llama/Llama-3.1-8B-Instruct)
- `Starling-LM-7B-beta/` 🤗 [link](https://huggingface.co/Nexusflow/Starling-LM-7B-beta)

Within each LLM folder, features are grouped by **rubric**.

#### Rubric Numbering Convention (ASAP dataset)

Each rubric folder is named using the format `rubric_<rubric_number>`. These rubric numbers are assigned based on the **first prompt ID** associated with that rubric.

For example, if a rubric is used for prompts 1 and 2, it is labeled as `rubric_1`.

Below is a mapping of traits to their associated prompts and rubric numbers:

| Trait             | Prompt IDs       | Rubric Numbers |
|------------------|------------------|----------------|
| organization      | [1, 2, 7, 8]      | [1, 7, 8]       |
| word_choice       | [1, 2, 8]         | [1]            |
| sentence_fluency  | [1, 2, 8]         | [1]            |
| prompt_adherence  | [3, 4, 5, 6]      | [3, 5]         |
| narrativity       | [3, 4, 5, 6]      | [3, 5]         |
| language          | [3, 4, 5, 6]      | [3, 5]         |
| conventions       | [1, 2, 7, 8]      | [1, 7]         |
| content           | [1–8]             | [1, 3, 5, 7]    |

> **Note:** The rubric number corresponds to the **first prompt ID** in the list of associated prompts.

The general file structure for the ASAP dataset is:

```plaintext
ASAP/
└── trait_name/
    └── LLM_name/
        └── rubric_<rubric_number>/
            ├── questions_<trait>.json
            └── ASAP_features_<trait>.csv
```

**File Descriptions:**

- `questions_<trait>.json` – Trait-specific questions extracted by the LLM during the **Rubric-based Feature Generation** stage.  
- `ASAP_features_<trait>.csv` – Trait-specific feature values computed during the **Feature Extraction** stage, based on the generated questions.  

---

### 📚 ELLIPSE Dataset

The `ELLIPSE/` folder follows the same file structure as `ASAP`, but **does not include rubric subfolders** as all essays are scored using a standardized rubric.  

The `ELLIPSE/` folder contains **six writing traits**:  

- `Cohesion/`
- `Syntax/`
- `Vocabulary/`
- `Grammar/`
- `Conventions/`
- `Phraseology/`

Each trait folder contains features extracted by **Starling-LM-7B-beta**.  

The `ELLIPSE/` folder also includes:  

- `ELLIPSE_data.csv` – Contains the generic writing-quality features (extracted using `features.py` and `create_readability_features.py` from https://github.com/robert1ridley/cross-prompt-trait-scoring), along with the assigned `prompt_id` and dataset `folds`.  

---

## 📜 Citation

If you use TRATES features in your research, please cite:  
```bibtex
@inproceedings{eltanbouly-etal-2025-trates,
    title = "{TRATES}: Trait-Specific Rubric-Assisted Cross-Prompt Essay Scoring",
    author = "Eltanbouly, Sohaila  and
      Albatarni, Salam  and
      Elsayed, Tamer",
    editor = "Che, Wanxiang  and
      Nabende, Joyce  and
      Shutova, Ekaterina  and
      Pilehvar, Mohammad Taher",
    booktitle = "Findings of the Association for Computational Linguistics: ACL 2025",
    month = jul,
    year = "2025",
    address = "Vienna, Austria",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2025.findings-acl.1054/",
    doi = "10.18653/v1/2025.findings-acl.1054",
    pages = "20528--20543",
    ISBN = "979-8-89176-256-5",
    }

