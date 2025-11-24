# 📘 OpenML Python – Contribution Portfolio  
### *Fixing Dataset Metadata Editing + Full Reproducible Notebook (ESoC 2025 Submission)*

This repository documents my contribution to the **OpenML Python** library as part of the **European Summer of Code (ESoC) 2025**.  
I implemented a bug fix for the `edit_dataset()` function and added a dedicated test + a full reproducible Jupyter notebook demonstrating the issue and the fix.

---

## 🚀 Contribution Summary

### ✔️ **Pull Request:**  
**Fix `edit_dataset()`: metadata list handling for creator/contributor/ignore_attribute**  
🔗 PR Link: https://github.com/openml/openml-python/pull/1488

This PR fixes a long-standing issue where updating metadata fields (like `creator`) would **silently fail** because the OpenML Python connector sent them as **plain strings**, while the server expects **list-style XML fields**.

I also added a new test:  

tests/test_edit_dataset_creator.py
---

## 🧩 What Was the Bug?

`edit_dataset()` used to serialize these fields incorrectly:

| Field | Old Behavior (Bug) | Expected Behavior |
|-------|--------------------|-------------------|
| creator | `"John"` (string ❌) | `["John"]` (list ✔️) |
| contributor | `"Jane"` | `["Jane"]` |
| ignore_attribute | string | always list |
| default_target_attribute | string | list |
| row_id_attribute | string | include only if not None |

Because of this mismatch, the OpenML server ignored updates silently — causing issue #1331.

---

## 🛠️ What My Fix Does

The fix ensures all affected metadata fields are properly wrapped in list-structured XML before sending to the server.

The PR includes:

- ✔️ Correct XML handling for metadata list fields  
- ✔️ New test ensuring metadata updates are applied correctly  
- ✔️ Notebook demonstrating before/after behavior  
- ✔️ Detailed PR explanation for maintainers  

---

## 📓 Jupyter Notebook Demonstration

A complete notebook is included:
notebooks/fix_edit_dataset_metadata_demo.ipynb
It demonstrates:

1. Creating a dummy dataset  
2. Publishing it to OpenML  
3. Showing the **buggy behavior** (before fix)  
4. Explaining server caching considerations  
5. Showing expected behavior after fix  
6. Notes about OpenML caching affecting immediate updates  

---

## 📸 Screenshots

### 🔹 Pull Request  
<img width="1801" height="955" alt="PR_Page_1" src="https://github.com/user-attachments/assets/6fc601f7-e737-4ded-9199-538bc922edde" />

### 🔹 Notebook Running  


<img width="1853" height="763" alt="notebook_running_1" src="https://github.com/user-attachments/assets/9d448f2b-1757-4d72-a438-9450fcb560f9" />
<img width="1867" height="748" alt="notebook_running_2" src="https://github.com/user-attachments/assets/27efc477-b78e-4ef7-ab04-6ccb9c8949b4" />
<img width="1852" height="707" alt="notebook_running_3" src="https://github.com/user-attachments/assets/e65b24b7-e1dd-43e7-ae15-cf08f9ad8a02" />

---

## 🧪 Test Added

### Test File:
tests/test_edit_dataset_creator.py
### Test Validation:

- Ensures XML is constructed using list-style metadata fields  
- Confirms `edit_dataset()` sends correct parameters  
- Ensures the server-side update function is called correctly  

### Test Result:

1 passed in 0.05s
---

## 📚 Technologies Demonstrated

- Python package development  
- Contributing to large OSS codebases  
- XML schema compliance  
- OpenML dataset publishing/editing  
- Writing unit tests with PyTest  
- Jupyter notebook demonstration  
- Real debugging + PR workflow  

---

## 🏆 Why This Contribution Matters

This bug impacted real OpenML users trying to update dataset metadata.  
My fix:

- Improves library reliability  
- Matches OpenML server expectations  
- Prevents silent failures  
- Adds long-term regression protection  
- Helps future contributors understand metadata structure requirements  

---

## 👤 Author  
**Ali Haider**  
ESoC 2025 Contributor – OpenML  
GitHub: https://github.com/alihaider-aischolar

---
