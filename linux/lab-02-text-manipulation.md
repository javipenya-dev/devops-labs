# Lab 02: Text Manipulation and Logs

**Date:** 24/11/2026
**Commands used:** `echo`, `cat`, `tail`, `grep`, `wc`

## What I did:
1. Created a dummy log file using `echo -e` to simulate server logs.
2. Read the whole file with `cat`.
3. Filtered the last lines using `tail -n 2`.
4. Extracted specific error messages using `grep "ERROR"`.
5. Counted total lines with `wc -l`.

## Why this matters for DevOps:
In real environments, logs are massive. Knowing how to filter (`grep`) and read the end of a file (`tail`) is essential for troubleshooting.
