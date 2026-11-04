# Classical Mechanics in Python

Lecture notebooks and examples for a university classical mechanics course.

Start with [the course contents](ClassMech_Python/classmech_TOC.ipynb), or
[open the contents in Google Colab](https://colab.research.google.com/github/kulinskij-tech/ClassMech/blob/main/ClassMech_Python/classmech_TOC.ipynb).

The collection contains 29 notebooks: 21 numbered lectures, seven supplementary
examples, and the contents notebook. Main teaching material is in English;
some supplementary notebooks are in Ukrainian. Topics include Lagrangian and
Hamiltonian mechanics, oscillations, averaging, self-oscillations, phase portraits,
first-order PDE characteristics, and action/entropy connections.

Every notebook has an Open in Colab badge. Exported notebook links open in Colab.
For local study, clone the repository, install the dependencies in
`ClassMech_Python/requirements.txt`, and open the notebooks with JupyterLab.

```sh
python -m pip install -r ClassMech_Python/requirements.txt
python -m jupyterlab ClassMech_Python
```

Run cells from the beginning. Interactive controls require an active Python kernel
and widget support. Imported lecture figures are embedded; no Mathematica runtime
is required. PDE exercises include closed hint/answer checkpoints.

These Python notebooks were adapted from the instructor's Wolfram materials and
subsequently expanded. Publication is generated through ColabGitEduAutomation
(CGEA); local authoring sources remain separate. See [source notes](SOURCE_NOTES.md)
for documented mathematical/source discrepancies and [validation](VALIDATION.md)
for the checks and limitations of this publication.

## Latest course update — 2026-11-05

The Hamiltonian lecture includes the new anisotropic-optics diagrams. The Poisson
lecture preserves the physics-first sequence and develops Lie structures afterwards,
using canonical q^i,p_i indices. The Hamilton–Jacobi notebook is marked as a draft
and includes additive separation, characteristic reconstruction, elliptic coordinates,
oscillator/pendulum/Kepler examples and self-study exercises with hidden checkpoints.
