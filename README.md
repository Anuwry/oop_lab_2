# OOP Lab 2 — CSV Data Processing

## Lab Overview
Goal: practice basic OOP for working with CSV data (cities & temperatures) using only Python’s standard library. 
The script loads Cities.csv, normalizes columns, lets me filter/select rows, 
compute a mean, and prints a few results (Germany rows, Spain rows with temp > 12°C, number of unique countries)

## Project Structure
oop_lab_2/
├─ README.md                # This file
├─ Cities.csv               # Dataset (UTF-8, header row)
└─ data_processing.py       # Classes + commit 3 oop_style

## Design Overview
### Helper func
_to_float(v) safe float parse; _norm_key(k) lowercases/strips keys; _norm_val(v) trims string cells. Used to keep data consistent
### Table
- State: self._rows: List[Dict[str, Any]] (all keys normalized)
- Key methods:
filter(predicate) -> Table, select(*cols) -> Table, mean(key) -> float|None, unique(key) -> List[Any], nunique(key) -> int, aggregate(key, agg_fn) These return new Table objects to allow chaining
### DataLoader
- load() -> Table: reads CSV via csv.DictReader, normalizes, returns Table
- from_common_locations() -> Table: searches ./Cities.csv, Cities.csv, /content/Cities.csv: raises FileNotFoundError if not found
### Script behavior (__main__)
- Load table (from common locations)
- Print average "temperature"
- Print rows where country == "Germany"
- Print rows where country == "Spain" and temperature > 12
- Print nunique("country")

## How to Run
bash - python data_processing.py ( Place Cities.csv next to the script )

IDE: upload the csv file then pulling it outta there by using the python code like my code in the lines 79 tap:
"""
def load(self) -> Table:
        rows: List[Dict[str, Any]] = []
        with open(self.path, newline="", encoding="utf-8") as f:
            reader = csv.DictReader(f)
            for r in reader:
                norm = {_norm_key(k): _norm_val(v) for k, v in r.items()}
                rows.append(norm)
        return Table(rows)
"""
