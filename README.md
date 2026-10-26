# Spheroid Demagnetization Factors

Micromagnetic calculation of the **demagnetization factor** of spheroidal
magnetic nanoparticles as a function of their aspect ratio, using
[Ubermag](https://ubermag.github.io/) / OOMMF.

The demagnetizing field is computed from the dipolar (demag) effective field
of a uniformly magnetized spheroid, and the resulting factor is compared with
the analytical formula for a prolate spheroid.

---

## Physics

For a uniformly magnetized body, the demagnetizing field is related to the
magnetization by

    H_demag = -N · M

and the corresponding demagnetizing energy is

    E_demag = (1/2) μ₀ V N · M²

where `N` is the demagnetization tensor and `V` the volume.

For a **prolate spheroid** of aspect ratio `m = c/a > 1` (semi-axis `c` along
the symmetry axis, semi-axis `a` in the transverse plane), uniformly
magnetized along the symmetry axis, the analytical demagnetization factor is

    N_z(m) = 1/(m² - 1) · [ (m / √(m² - 1)) ·
             ln( (m + √(m² - 1)) / (m - √(m² - 1)) ) - 1 ]

with the limiting case for a sphere (`m = 1`):

    N_z(1) = 1/3

The simulation computes `N_z` from the average demagnetizing field along `z`:

    N_z = -⟨H_demag,z⟩ / M_s

---

## Model

Each simulation cell is a nanoparticle. The energy contains only:

- **Zeeman** (uniform saturating field `H₀` along `z`)
- **Demag** (dipolar interactions)

> ⚠️ Exchange and anisotropy terms are **not included**: the purpose is to
> obtain the demagnetization factor of a uniformly magnetized body.

The simulation runs at `temp = 0` (no thermal noise) with Gilbert damping
`alpha = 0.5`.

---

## Requirements

- Python 3.9+
- [Ubermag](https://ubermag.github.io/) (`oommfc`, `discretisedfield`, `micromagneticmodel`)
- **OOMMF** installed and available in `PATH`
  (see [OOMMF installation guide](https://math.nist.gov/oommf/))
- `numpy`, `matplotlib`

---

## Installation

Clone the repository and install the Python dependencies:

```bash
git clone https://github.com/<usuario>/<repo>.git
cd <repo>
pip install -r requirements.txt
