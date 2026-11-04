# Source discrepancies: stationary-action examples

The Python inputs follow the executable definitions in `action0.nb` and `class_action0.nb`.
The displayed lecture equations remain as written in the originals. Original cell contents
and identifiers are also retained in notebook cell metadata. Language edits preserve meaning.

- Several display equations use `(gt)^2` or `(gx)^2` where the executable trajectory uses
  `g t^2` or `g x^2`. These expressions coincide in the chosen units `g=1`, but differ otherwise.
- The displayed perturbation is `sum(sin(pi*k)/k^2, k=1..2)`, without a position variable.
  That sum is identically zero. The executable source instead uses
  `sum(sin(pi*k*x)/k^2, k=1..2)` with normalized position `x` in `[0,1]`.
  Python follows this executable definition, including its endpoint conditions.
- The action is the fixed-energy abbreviated action `integral p ds`, not the fixed-time
  Hamilton action `integral (T-U) dt`.
- Some slider/perturbation combinations cross `y=1=E` and make the source momentum complex.
  The Python plot leaves gaps for these inadmissible paths and labels the table accordingly.
  It does not clip the square root, take an absolute value, or change the source angle range.
- The concluding prose discusses minima, maxima, and inflection points. This statement is
  preserved and only edited for language; a one-parameter perturbation plot alone does not
  classify the second variation over all admissible paths.

These notes separate conversion choices and mathematical issues from the lecture narrative.

## Mathematical pendulum

- The source uses `omega=1/sqrt(2)` in the quadrature/period cells, then `omega=1`
  in the `DSolve`/animation and phase-portrait cells. Python preserves these separate
  time conventions instead of silently applying one scale throughout.
- The displayed time-angle equation has the opposite sign to the executable `tpend`
  definition. Python follows `tpend`, so elapsed time from the upper turning point is positive.
- The source integration assumptions include `phi >= phi0`, whereas the real libration
  branch used in the period computation has `abs(phi) <= phi0`. Python evaluates
  that real branch using an equivalent elliptic-integral parameter in `[0,1)`.
- The narrative's comparison with `m g l` and its quoted critical speed are retained.
  For the energy convention in the phase-portrait code, the separatrix is at `E=2`
  and dimensionless initial speed `v0=2`; an energy measured from the lowest point
  has the physical barrier `2 m g l`.
- The dashed turning-angle line is drawn only for finite motion, because
  `2 asin(v0/2)` becomes complex above the separatrix. The physical trajectory is
  computed in all three regimes. The animation uses a play control and time slider;
  its repeat setting is continuous rather than the source's three repetitions.
- The original pendulum code uses a rainbow colour scheme for the phase portrait;
  Python retains it and additionally marks the separatrix in black.

## Hamilton–Jacobi lecture

The source has no computational input cells. All text and displayed equations are
transferred in order, with equation references updated to the five numbered equations.
The lecture ends with “Let’s illustrate this” but contains no subsequent example;
the conversion does not invent one. The displayed type-2 generating-function equation
retains the original signs of its `H dt` terms, which merit a separate mathematical review.

## Poisson brackets

- The notebook's `CellPrint` headings and cached symbolic outputs are separate source cells.
  Python preserves those positions: definitions occupy the original inputs, followed by
  headings and Python cells that regenerate each original symbolic output.
- With `H=p^2/(2 mu)-gamma/r` and `A=p cross L-mu gamma r/r`, the norm identity is
  `A^2=mu^2 gamma^2+2 mu H L^2`. The original intermediate expression subtracts
  `gamma^2` and divides by `2 H`, omitting mass factors. Python evaluates that expression
  literally as `source_identity_residual` and separately verifies the identity with
  the correct factors. The lecture's displayed formulas remain as written.
- The Runge–Lenz brackets are checked with the same mass convention:
  `{A_i,A_j}=-2 mu H epsilon_ijk L_k`.
- The brief recurrence statement in the source is preserved; a complete mathematical
  statement of recurrence would require qualifications beyond this language-edit scope.

## Generalized coordinates

The original acceleration computations differentiate velocity with respect to the coordinates
while holding their rates fixed. They calculate the quadratic (convective) term. The general
acceleration also includes `J*q_ddot`, as the lecture's theoretical formulas state. The Python
cells preserve this assumption explicitly. Trigonometric norm simplification uses polynomial
identities to keep the exact three-dimensional expressions quick to evaluate. Singular points
are omitted from plots rather than replaced with finite coordinates.

## Differential geometry of curves

The helix code defines torsion using `r''' dot (r'' cross r')`, the negative of the usual
Frenet–Serret convention used in its adjacent formulas. Its red Darboux arrow is reproduced
with this original sign and labelled accordingly. The initial still frame shows a full turn
so that the curve is visible; the original parameter range remains available in the controls.

The prose's claim that equations of motion must be of order at most three does not follow from
the curvature and torsion formulas. The statement is retained with that qualification. Likewise,
torsion is not defined by the Frenet frame on a straight line where curvature vanishes. The
arc-length interpretation of an evolute's curvature-radius parameter is local to monotonic
segments. These qualifications are made explicit in the edited prose.

## Stationary-action lecture

The squared radial first-order ODE allows more branches than the intended nonconstant straight
geodesic; the notebook displays the nonconstant branch and the constant branch and notes this
distinction. The source's cycloid multi-point interpolation is reproduced as an illustration,
not asserted to solve the tautochrone dynamics. Its `ssqrt` typo is interpreted as `s*sqrt`.
The double-pendulum position vectors used to compute kinetic energy differ by a common rotation
from the gravity-aligned drawing; this does not change kinetic energy. Potential energy uses
the source's cosine convention. A cached Input-style double-pendulum widget is regenerated.

## Equations of motion

The double-pendulum parameters, initial state, and time interval match the source. SciPy's
adaptive DOP853 method replaces `NDSolve`; conservation of the stated energy is checked.
Long chaotic trajectories need not agree point by point with a saved Wolfram trajectory.
The two-mass problem's “string with stiffness” is rendered as “spring,” as its title indicates.

## Central fields

The displayed integrals and turning points are reproduced with their original normalization.
The two-body animation uses eccentricity `ex=0.75` but reuses the preceding angular solution
for `e0=0.8`, as the source does. It therefore illustrates the centre-of-mass geometry rather
than a consistently timed Kepler orbit at `ex=0.75`. Its plotting bounds are slightly widened
to show the second body's entire orbit. The earlier single-orbit animation has consistent
eccentricity and is checked independently. The Input-style saved animation is regenerated.

## Scattering

All five original raster figures are embedded as PNG attachments. Decoded pixels are checked
byte for byte after PNG encoding. The introductory language distinguishes kinetic-energy
conservation in elastic collisions from conversion to other forms in inelastic collisions;
total energy conservation is not denied. No figure is replaced with a newly drawn approximation.

## Rigid-body mechanics and the additional top notebook

The rotation convention is intrinsic ZXZ. The symbolic calculations independently compare
angular velocity obtained by adding the three angle-rate contributions with the axial vector
of `R_dot R.T`, and transform it to the body frame. Uniform-body inertia tensors are derived
by integration or the exact covariance of a filled simplex. The triangle, cube, sphere,
solid ball, and unit-edge regular tetrahedron reproduce the source examples.

The source's layered tetrahedron drawing uses vertices that do not form a regular tetrahedron.
Those vertices are preserved in the illustration; the regular-tetrahedron inertia calculation
uses a genuinely regular tetrahedron. The numerical free-rotation example uses the original
moments `(1,2,4)`, initial angular velocity `(-0.1,1,0.1)`, and interval `[0,30]`.
Its displayed ellipsoid retains the source radii `1/I`, although the conventional inertia
ellipsoid has radii proportional to `1/sqrt(I)`. Energy and angular momentum conservation
are checked. The invariant-surface plot is widened to show both complete surfaces; the
source's rigid-body version clipped them to a cube with half-width 0.75.

The separate `classmech_top` filename and title are retained even though its supplied content
mostly develops inertia and torque-free rotation, rather than a full heavy-top solution.
The prose identifies a homogeneous cube as a spherical top and corrects minor terminology.

## Symmetric top

The source calls an inverse-function symbolic solver for generic Euler equations and records
an incomplete-inverse-function warning. Python gives an explicit quadrature after eliminating
two squared components using the energy and angular momentum integrals. It states the branch
sign, distinct-moment assumption, and separate principal-axis equilibria. Thus the solution
remains in quadratures without requiring a proprietary symbolic solver. The source's elliptic
function derivation and formulas are retained, followed by the symmetric and heavy-top cases.

The four original diagrams are embedded. The effective-potential control shows the original
parameter ranges, with numerical turning points. The source's blanket claim of stability at
zero nutation angle is qualified: compatible momenta and sufficient spin are required.

## Quaternions

The second source matrix has `x0` in its lower-right element, where the quaternion definition
requires `y0`. The literal matrix product is retained, and the corrected product is shown
separately. Python checks the multiplication homomorphism, norm identity, invariant rotation
axis, and the explicit z-axis rotation. The polynomial rotation matrix is labelled as a
unit-quaternion expression; the underlying rotation function divides by the norm squared.

## Lattice oscillations

The monoatomic and diatomic dispersion functions preserve the original parameters and controls.
The source's plot over negative wave vectors shows positive `2*abs(sin(q/2))` but uses the
signed-branch expressions for the phase and group velocities. Python preserves those two
curves with explicit formula labels and explains the sign difference. The removable singularity
at zero wave vector is evaluated by its limit. All four original chain diagrams are embedded.
The optical-mode explanation is qualified to distinguish general optical modes from their
coupling to light in polar crystals.

## Hamiltonian mechanics and optics

The Legendre-transform prose states the strict-convexity and existence assumptions. The
Hamilton–Jacobi normal-direction statement is limited to isotropic kinetic energy. The
secondary-wave illustration preserves the original plane at `t/2` and spheres of radius `t`,
and explicitly notes that the plane is not their envelope. The original refraction arrow
uses `asin(1/n)` independently of incidence; that arrow is retained while a separate numerical
comparison gives Snell's angle for the actual incident beam. These source illustrations
should not be interpreted as fully consistent wavefront simulations. Random point-source
directions use a fixed seed for reproducible output. Three original raster figures are embedded.

## Nonlinear oscillations

On 2026-10-04, at the user's request, the high-frequency external-force subsection
(original source cells 55–81, including the Kapitsa example) is moved into
`classmech_oscphdiag.ipynb` after mechanical forcing and before harmonic circuits.
The original text, formulas, figure attachments, computation parameters, and raw
source metadata are retained; equation labels change from 9–16 to HF1–HF8, with
the relevant prose references updated. Moved cells identify their original notebook
in provenance metadata. A local SciPy import makes the example independent of the
nonlinear notebook's setup. The nonlinear notebook links to the new location.
The current notebook already omitted later source prose cells 82–83 before this
move; these existing edits are preserved. The Kapitsa parameter drift described
in VALIDATION.md is unchanged and now concerns the moved example.

The frequency correction is derived with a fixed phase variable to avoid ambiguity in expanding
the frequency inside trigonometric arguments. It yields `3*b/8 - 5*a**2/12`. The original
particular solutions and numerical example with unit initial displacement are retained.
The source's perturbative comparison uses amplitude one, outside a reliably small-amplitude
regime, and its approximate initial displacement differs from one; the code makes this explicit.

The Kapitsa simulation derives the equation from the original Lagrangian. That Lagrangian uses
`y+cos(phi)` and gives `phi_ddot=-(1-y_ddot)*sin(phi)`, while the original drawing uses
`y-cos(phi)`. Both source conventions are preserved and identified. A small integration step
resolves the rapid drive. The final source Wolfram Cloud error is represented by a comment
at its original position; no cloud connection is needed. The source's later self-oscillation
paragraph is retained, including its attribution.

At the user's request (2026-10-01), the earlier auto-oscillation subsection is expanded
with new teaching material, separately marked in cell metadata. It covers van der Pol
and Rayleigh models, energy balance, weak-damping amplitude selection, relaxation
oscillations, common physical examples, and the local Stuart–Landau amplitude model.
Three executable plots illustrate transients, parameter dependence, and the two forms
of nonlinear damping. Original source cells remain in their original relative order.
The builder inserts the same extension on regeneration; this is additional material,
not a claim that these calculations appeared in the Wolfram source.

## Normal modes and the additional parameter-named notebook

The double-pendulum example divides both its mass and stiffness matrices by two; this common
factor cancels in the generalized eigenvalue problem and is retained. The source expands to
second order in each angle separately, which can retain higher total-degree terms. Python
retains this rectangular expansion and evaluates the Hessians at equilibrium for the linear
modes. The coupled-pendulum strong-coupling limit has one finite in-phase frequency and one
diverging frequency. Ring modes are verified against `K v = omega^2 M v`.

Eigenvector ordering, normalization, and bases in degenerate subspaces are not unique.
The triangular-molecule example keeps the source's negative coefficient-matrix eigenvalues
and reproduces its breathing-mode normalization; a different valid basis may span the
twofold-degenerate modes. The Jordan-form prose corrects the spelling of Cayley–Hamilton
and distinguishes algebraic multiplicity, Jordan-chain lengths, diagonalizability, and
indecomposability. The original formulas and exercise sequence remain available.

`classmech_parametricres.nb` actually contains another set of normal-mode examples and an
optional Rubi package-location query. Its filename and source content are retained. The
package query is replaced with identification of the open-source SymPy backend; the source's
commented installation instruction is not run. No absent parametric-resonance lecture is invented.

## Operational calculus

Laplace transforms, initial-value terms, circuit equations, and periodic-switching limits are
computed with SymPy. A three-pulse transform is obtained by integrating its active intervals,
equivalent to the source's step-function calculation. The zero-frequency limit of the periodic
response is identified as its mean, not a pointwise final value. The last source expression is
the full transform, containing both mean and alternating parts, and is labelled accordingly.
The introductory description of complex scaling is restricted to individual complex-exponential
components; arbitrary real linear maps are not all rotations and dilations.

Two source circuit images are embedded losslessly. The third circuit is encoded as explicit
Bezier outlines, including its letter shapes; those original paths are rendered with Matplotlib.
Packed coordinate arrays are decoded directly, with segment and point counts checked.

## Complex numbers, phasors, and impedance

All sixteen computational/source-graphic inputs are covered. The animation controls retain
their parameter ranges; static snapshots use useful representative phases. The beats example
embeds ten seconds of 440 Hz and 440.5 Hz sound in a player with no autoplay. Forced oscillations
use the exact analytic resonant limit when the driving frequency equals the natural frequency.
The damped-response peak is placed at zero when damping exceeds the finite-frequency-peak
threshold, avoiding a failed numerical minimization.

The phase table explicitly states that its signs refer to current relative to voltage. The
displacement phase-lag prose is corrected to span zero to pi with the correct quadrant. The
source's positive-square-root initial-velocity formula is preserved and its phase-sign ambiguity
is explained. The constant-energy exercise is qualified: equality of average energies alone
does not determine the driving frequency. The Joule-power prose restores the missing square
on voltage amplitude, with that correction stated in the notebook. Frequency-independent
current amplitude constrains the magnitude of impedance, not necessarily its phase.

The source's imported PDF diagrams are already present as cached raster images. These original
pixels are embedded in Python display cells, whose long image-data code is initially collapsed.
All other original illustrations are embedded as Markdown attachments. No external PDF assets
or Wolfram figure imports are required when the notebook is rerun.

## Source inventory and final formatting

Four current source files differed from the earlier inventory when this continuation reviewed
them: nonlinear oscillations, operational calculus, lattice oscillations, and phasor diagrams.
The previous records are retained in `previous_source_inventory.json`; the current inventory
and notebook audit trails use the current source files. Conversion scripts do not modify the
Wolfram notebooks. Source caches are now keyed by file hash to prevent reuse after source edits.

Visible curly brackets are escaped only at source-string leaves, before LaTeX command grouping
is generated. This preserves grouping braces in fractions, indices, and other commands.
The course contents has one numbered level, 1–17, with the five additional examples linked below.

### Markdown parenthesis formatting

Math parentheses now use `\left(` and `\right)` throughout the delivered notebooks.
Existing explicitly sized pairs are preserved. Delimiter-only bold groups from Wolfram
styling are removed where necessary so each pair belongs to the same LaTeX group.
Prose parentheses and all Python code, outputs, figures, and source metadata are preserved.

Five source passages had an opening parenthesis inside inline math and the closing one
outside it; the closing delimiters are moved into math. The characteristic-polynomial
aside in the normal-mode lecture instead keeps both outer parentheses in prose.
Two unmatched closing parentheses inside square roots in central-field source cell 54
are removed. Hamiltonian source cell 40 gains the missing opening parenthesis enclosing
both terms of its final variational integral. These are delimiter repairs; the original
source expressions remain in cell metadata.

The same sizing convention is applied to square brackets, visible braces, absolute-value
bars, and angle brackets. Delimiter-only groups on closing absolute-value bars are removed
so squared magnitudes display correctly. Evaluation bars with limits use `\left.` and
`\right|`; cases use `\left\{` and `\right.`. These one-sided delimiters are not converted
into paired absolute values or given artificial visible closing braces.

### Trigonometric notation

Prose annotations and descriptive labels inside mathematics use `\text{...}`.
This includes the phasor example `\text{speed of }\dot{Z}=\text{acceleration}`,
matrix descriptions, Euler-angle names, and effective/kinetic-energy labels.
The reviewed vocabulary leaves mathematical variables and operators intact and
protects existing text commands. Fifty-one Markdown cells in fourteen notebooks
are updated without changing code, outputs, or source metadata.

Limit operators use `\lim\limits_{...}` rather than `\underset{...}{lim}`,
as requested. Three occurrences in central-field and operational-calculus Markdown
are updated; the source renderer also emits this notation on regeneration.

Trigonometric, inverse-trigonometric, and hyperbolic function names are formatted with
LaTeX commands and grouped arguments, including `\sin{\omega t}` and `\cos^{2}{\theta}`.
Wolfram-style `Sin[...]`, `Cos[...]`, and `Csc[...]` are converted to ordinary mathematical
notation, and the source abbreviation `ctg` becomes `\cot`. Existing visible parentheses
on function arguments retain their automatic sizing. Angular subscripts enclosed with a
function name by a source SubscriptBox are moved onto the angle inside the function's
argument. Outside factors, such as the x in `(tan alpha)*x`, remain outside the argument.
Two argument-free sine/cosine names in a source explanatory annotation remain standalone
operator names. Notebook code, outputs, figures, and original source metadata are preserved.


### Phase portraits and ecological oscillations — 2026-10-07

The user explicitly requested additions in both `classmech_nlosc.nb` and its
Python twin. Added phase-plane definitions, nullclines, Jacobian/eigenvalue
classification, six illustrated linear fixed-point types, the van der Pol
classification, and ecology-motivated Lotka–Volterra dynamics with symbolic and
numerical examples. Purely imaginary eigenvalues alone do not prove a nonlinear
centre; the Lotka–Volterra first integral supplies the extra argument.

Classical Lotka–Volterra is not presented as an attracting self-oscillator: it
has neutral periodic orbits with amplitudes selected by initial conditions.
The added Rosenzweig–MacArthur comparison illustrates an attracting ecological
limit cycle. The scaled model with d=1/2 has coexistence at (1, 2(1-1/K)),
trace (K-3)/(2K), determinant (K-1)/(4K), and Hopf threshold K=3.
References are linked in both notebooks (MIT/Rosales notes on the first integral
and University of Amsterdam/de Roos notes on the ecological Hopf bifurcation).

All 50 existing Python cell sources and all 65 existing Wolfram cells were
preserved. The Python notebook executed completely; four new Wolfram examples
executed locally with saved native outputs. Independent symbolic and numerical
checks pass; phase portraits and native formulas were visually inspected.
See PROJECT_CONTEXT.md for the checks, backups, and stale-builder warning.


### Averaging method revision — 2026-10-08

At the user's request, the first nonlinear-oscillation section in both formats
now uses the averaging method, guided by the attached `averaging.pdf` (UConn
Physics 2400, Spring 2017). General nonlinear Lagrangian terms, overtones,
combination frequencies and secular motivation are retained. The old detailed
successive-approximation worked example is replaced by slow amplitude/phase
derivations and cubic damping, Duffing and adiabatic examples. Its quadratic/
cubic frequency shift is retained as a higher-order connection. The harmonic
Lagrangian now groups both kinetic and potential terms under the one-half factor.

The lecture uses one sign convention, x''+x=epsilon*F, throughout. Exact polar
coordinates and approximate averaged variables are distinguished; leading state
reconstruction is not claimed to satisfy the derivative identity beyond its
order. The notes' general higher-order recurrence in Eq. (8) is not reproduced:
the full nonlinear product must be expanded. The varying-frequency action is
approximately conserved, and the dry-friction exercise distinguishes sliding
from sticking. Numerical comparisons use matched leading state data and display
sampled errors over fixed slow time. No PDF diagrams are imported: outputs are
regenerated in Python and Wolfram Language.

The complete Python lecture and all five new native Wolfram examples execute.
Independent reference-solver, energy-balance and period checks pass. New plots
and native formulas were inspected. See PROJECT_CONTEXT.md for current counts,
error values, preservation checks, backups and rebuild limitations.


### Separate auto-oscillation Python lecture — 2026-10-08

Mirrored the user's new `classmech_autosc.nb` by transferring the phase portraits,
self-oscillation and ecological material into `classmech_autosc.ipynb`. The
nonlinear/harmonic introduction and averaging comparisons remain in
`classmech_nlosc.ipynb`. Existing source text and code are preserved; the
self-oscillation introduction now precedes phase portraits, matching Wolfram.
Both notebooks run independently. The ToC has 19 flat numbered entries and both
notebooks have reciprocal navigation. Original provenance metadata is historical;
moved-cell origin is explicitly recorded. No Wolfram source was changed by this
Python restructuring. Preservation, saved-output and link checks pass.

## Lie groups and Lie algebras introduction — 2026-10-30

Added a matching introductory section to `classmech_poisson.ipynb` and its native
`.nb` twin, ahead of the original phase-space discussion. The sequence is vector
fields as derivations, cancellation of second derivatives in their commutator,
translation/shear example, Lie algebra axioms and structure constants, Lie group
and tangent algebra, matrix exponentials, translations/SO(2)/SO(3), and Poisson
observables/Hamiltonian generators. Included three closed answer checkpoints and
independent symbolic examples in both runtimes. Explained the convention
X_f h={h,f}, for which [X_f,X_g]=-X_{ {f,g} }; constants are in the kernel.

Corrected two existing displayed definition typos in both formats: the last
antisymmetry term in equation (2) is -{H,f}, not -{f,H}; equation (6) now uses
{g,f}=sum(g_q f_p-g_p f_q), consistent with the existing poiss implementation and
{q,p}=1. Original native contents remain in dated backups for provenance.

Validation on Windows, 2026-10-30: full expanded Python notebook executed freshly,
new code assertions and an additional Jacobi check passed, schema/no-error checks
passed; local Mathematica examples passed and the finished native notebook loads.
39 new native cells; all original native cells preserved except the two corrected
definitions. Existing Python code sources preserved. No full frontend visual audit.
Reference: MIT OCW 18.745 Lie Groups and Lie Algebras I lecture notes:
https://ocw.mit.edu/courses/18-745-lie-groups-and-lie-algebras-i-fall-2020/resources/lecture-notes/

Placement clarification, 2026-10-30: the Lie-theory addition now follows all
original physical material and is titled “Mathematical structures emerging from
Hamiltonian mechanics”. Original physics cells/order, outputs and the two sign
corrections were preserved. Mathematical terminology is developed from the
mechanical constructions already presented, rather than imposed beforehand.

Canonical-index clarification, 2026-10-30: all general Poisson definitions use
q^i,p_i, {q^i,p_j}=delta^i_j. This mixed Kronecker delta represents canonical
pairing, not a metric. The associated antisymmetric Poisson bivector and zero
coordinate-coordinate/momentum-momentum brackets are now explicit in both formats.
One-dimensional suppressed-index examples remain unchanged.
