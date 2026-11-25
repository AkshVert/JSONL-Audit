JSONL Audit
A dependency-free Python CLI for validating JSON Lines datasets before feeding them into GenAI training, evaluation or data pipelines.
Features
- Streaming, line-by-line processing without retaining records.
- Detects malformed JSON, blank lines, non-object records and missing/null required fields.
- Rejects nonstandard NaN and Infinity literals.
- Reports field frequency and bounded error examples with line numbers, without exposing record contents.
- JSON reports and CI-friendly exit codes.
Quick start
Requires Python 3.10+. From the project directory:
python -m jsonl_audit sample.jsonl --require prompt --require response --output report.json
The intentionally flawed sample contains four lines: two valid, one missing a required field and one malformed. Exit codes: 0 = clean, 1 = invalid records, 2 = usage or I/O failure.

Optional installation: python -m pip install . then use jsonl-audit.
Architecture
Input stream → strict JSON parsing → object/required-field validation → counters → JSON report.

Memory scales with the longest record, distinct field names and configured example limit, rather than total record count. Required fields are checked for presence and non-null values, not types or semantic correctness. This is a structural quality check, not a complete training-data evaluation. Duplicate JSON keys are not detected.
Testing
python -m unittest discover -s tests -v
GitHub Actions runs tests on Python 3.10, 3.12 and 3.13.
Roadmap
JSON Schema validation, duplicate detection, dataset splitting and token statistics.
