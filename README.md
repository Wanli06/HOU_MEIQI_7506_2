# DASE7506 MP2 - frozen fifth-study submission

Official test accuracy: **389/467 = 83.29764453961457%**. Validation: 744/798 = 93.23308270676692%. The requested 84% target remains unmet. All inference assets are included in `code/checkpoints/final_v5` (12,494,458 bytes). The selected method is `code/submission_v5.py`; its SHA-256 freeze is `code/checkpoints/freeze_v5.json`.

Read `report/DASE7506_MP2_Final_V5_Report.pdf` (five pages) and `AI_USE.md`. The report documents all nine new comparisons, earlier failed studies, adaptive training-only CV, prior known aggregate benchmark results, and the explicit pre-test decision to abandon the assistant's non-official 82.8% internal gate. One new official test evaluation followed freezing; no post-test model tuning occurred.

## Restore original course data and reproduce without retraining

The original supplied data is omitted from this browser-upload snapshot because its training embedding file exceeds GitHub's 25 MiB browser limit. All learned model assets are present. `download_course_data.py` downloads only the official course repository data and verifies every file against the supplied, included manifest. It downloads no external model weights or extra training examples. Alternatively copy the original official `code/data` files here, preserving the supplied license and notice.

Python 3.12, from the repository root (PowerShell):

```powershell
py -3.12 -m venv .venv
.\.venv\Scripts\python.exe -m pip install numpy==2.5.3 scipy==1.18.1 scikit-learn==1.9.1 threadpoolctl==3.7.0
Set-Location code
..\.venv\Scripts\python.exe download_course_data.py
..\.venv\Scripts\python.exe check_data.py
$env:OMP_NUM_THREADS='4'
$env:OPENBLAS_NUM_THREADS='4'
$env:MKL_NUM_THREADS='4'
$env:NUMEXPR_NUM_THREADS='4'
..\.venv\Scripts\python.exe predict.py --method submission_v5.py --checkpoint checkpoints/final_v5 --split test --output results/reproduction-v5/test-predictions.json
..\.venv\Scripts\python.exe score_predictions.py --split test --predictions results/reproduction-v5/test-predictions.json --output results/reproduction-v5/test-score.json
```

The saved official outputs are `code/results/final_v5/test-predictions.json` and `test-score.json`. Complete local fresh-process prediction plus independent scoring took 6.557273600017652 seconds on an i9-13900HX CPU, with four threads. The reference Xeon was not measured.

## Reproduce training and review evidence

All training/inference Python sources, prior frozen checkpoints, fourth/fifth-study internal evidence and fifth-study official outputs are included. Study-5 fitting needs only the pinned NumPy/SciPy/scikit-learn/threadpoolctl environment above and the restored original data. Run `train_v5.py` from `code` to regenerate six direct configurations and three mixtures. Previous training-only OOF artifacts in `results/v4` are the fixed prior's development inputs; they are never inference lookups.

`finalize_v5.py` refits, checks, freezes and evaluates the selected model; it refuses to overwrite `checkpoints/final_v5`. To recreate a new research freeze, use a separate copy and preserve the supplied official frozen assets and score records. Earlier full-study training recipes use additional training-only libraries listed in `requirements-v4-training-lock.txt`; PyTorch/LightGBM/CatBoost are not needed for current frozen inference. The complete earlier local archives contain additional historical reports and validation experiments beyond this browser snapshot.

Keep the supplied `code/data/LICENSE.txt` and `NOTICE.txt`. Official guide: https://github.com/xudongwu-0/DASE7506-MP2/blob/main/guide/GUIDE.md . The student must supply their own identity and submission URLs and review/understand the substantive AI-assisted work. No publication or coursework submission was performed by the preparation script.
