# Raw data format

One tab-separated text file per tightening run. Copy the folders from
`OneDrive\Desktop\raw_data_steel\` into `data/raw/` locally. They are git-ignored.

## Header (3 lines, CP949 / EUC-KR encoding)

```
측정명/지그:OUTLET
측정시간:2026년03월20일-19시17분        측정자: Enkh Amar
 Load Peak(Kgf) : 0    Torque Peak(N.m)  : 0
```

Read it with `encoding="cp949"`. With the default UTF-8 the Korean turns into garbage.

## Body (3 columns, no header row)

| Column | Meaning | Unit |
|---|---|---|
| 0 | sample index | – |
| 1 | clamp load | kgf (× 9.80665 → N) |
| 2 | torque | N·m |

Example: `ConfigA-50_1.txt` has 13,500 rows, peak load ≈ 945 kgf (≈ 9.27 kN), and peak torque ≈ 48.9 N·m.

## File names

| Pattern | Example | Meaning |
|---|---|---|
| `ConfigA-{torque}_{repeat}.txt` | `ConfigA-50_1.txt` | Config A, 50 N·m target, repeat 1 |
| `YYYYMMDD-{torque}_{repeat}.txt` | `20260321-70_3.txt` | Config B/C (the folder tells you which) |
| `ConfigB_{torque}_{repeat}.txt` | `ConfigB_90_2.txt` | Config B, 90 N·m |
| `YYYYMMDD-HHMM_mu_{ss\|b}_{torque}_{repeat}.txt` | `20260410-1607_mu_ss_50_1.txt` | lubrication series |

Parse the target torque and repeat number from the file name with a regular expression,
and take the configuration from the folder name.

## Notes to fill in

- Bolt nominal diameter *d* used for *K*: *TODO* (the week-1 script assumed 12 mm. Check the thesis.)
- What exactly differs between Config A, B and C: *TODO*
- Known bad runs to exclude, and why: *TODO*
