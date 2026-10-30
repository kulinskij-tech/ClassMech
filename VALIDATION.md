# Publication validation — 2026-10-30

CGEA repo-aware export, Windows, branch main, ClassMech_Python course folder.

- 29 notebooks exported from the complete source inventory, including the ToC.
- Every export compared exactly with the source plus the CGEA transformations:
  one Colab badge and rewritten notebook links. Source notebooks preserved by export.
- 54 local notebook navigation links checked; no unresolved local resources.
- All nonempty code cells passed Python syntax parsing; no saved error outputs remain.
- A plotting-title escape error in the supplementary symmetry notebook was fixed
  in the authoring source and the notebook executed in a fresh local kernel.
- PDE exercise solutions and native notebook loading were checked in prior targeted
  work. Eight affected core notebooks passed fresh execution on October 28.
- All imported figures are embedded; existing images, code, metadata and outputs
  are retained by the exporter. Course requirements and source notes are included.

Limitations: no full fresh execution of every notebook in this publication run,
no live Colab execution, and no complete browser/MathJax rendering audit. The
exporter's badge cell follows its existing format without a cell id. Earlier
execution checks are historical evidence, not fresh execution of the whole course.
The original .nb files, reference books, PDFs, caches and migration runtime are
not part of this Python publication. No license is inferred for source references.
