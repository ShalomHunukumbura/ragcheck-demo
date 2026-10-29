# ragcheck-demo

A small RAG pipeline (a shop's help centre: refunds, delivery, warranty, payments,
accounts) guarded by the [ragcheck](https://github.com/ShalomHunukumbura/ragcheck) GitHub
Action. Every pull request runs five known questions through the pipeline and fails if an
expected answer, its supporting text, or the right document goes missing.

**The open pull request** trims each document to its first sentence to send the model less
text. It's a one-line change that looks like an easy win. ragcheck blocks it: four of the
five answers are gone.

## Run it locally

```bash
pip install ragcheck-ci
export RAGCHECK_DATASET=eval/questions.jsonl
export RAGCHECK_PREDICTIONS=/tmp/predictions.jsonl
python app/run_pipeline.py
ragcheck-ci --dataset "$RAGCHECK_DATASET" --predictions "$RAGCHECK_PREDICTIONS" --k 3
```

To see the failure, apply the pull request's change: `git apply regression.patch`.
