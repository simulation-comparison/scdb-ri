# Energy conservation — EGSnrc <!-- omit in toc -->

⚖️ [scdb-ri/20251015-energy-conservation](https://github.com/simulation-comparison/scdb-ri/tree/main/comparisons/20251015-energy-conservation)

## Table of contents  <!-- omit in toc -->

- [1. Software](#1-software)
- [2. Reproducibility](#2-reproducibility)
- [3. Geometry](#3-geometry)
- [4. Materials](#4-materials)
- [5. Source](#5-source)
- [6. Scoring](#6-scoring)
- [7. Parameters](#7-parameters)
- [8. Results](#8-results)


## 1. Software

The EGSnrc simulations were carried out with [EGSnrc 2025a](https://github.com/nrc-cnrc/EGSnrc/tree/v2025a) (commit [79890aa](https://github.com/nrc-cnrc/EGSnrc/commit/79890aaaeebced4bc136820028d83a448b1b4a3f)) without modification. This version was released on March 14, 2025.

## 2. Reproducibility

To reproduce the simulations presented here:

1. Install EGSnrc as per the [EGSnrc installation instructions](https://github.com/nrc-cnrc/EGSnrc/wiki/Installation-overview).

2. Compile the `egs_app` application:

   ```bash
   cd $EGS_HOME/egs_app/
   make
   ```

3. Download any EGSnrc input file from this comparison to the `$EGS_HOME/egs_app/` directory.

4. Run the simulation:

   ```bash
   egs_app -i 20251015-electrons-Z006-0.010MeV.egsinp
   ```

## 3. Geometry

The unbounded simulation space is modelled using the [`egs_space`](https://github.com/nrc-cnrc/EGSnrc/blob/master/HEN_HOUSE/egs%2B%2B/geometry/egs_space/egs_space.h) geometry. Technically, this geometry always returns a [very large distance](https://github.com/nrc-cnrc/EGSnrc/blob/79890aaaeebced4bc136820028d83a448b1b4a3f/HEN_HOUSE/egs%2B%2B/egs_functions.h#L105) ($10^{30}$ cm) when its `howfar()` and `hownear()` methods are invoked, effectively modelling an unbounded space.

Here is the geometry input block template used for all simulations in this comparison:

```ruby
:start geometry definition:

    :start geometry:
        name = space
        library = egs_space
        :start media input:
            media = %(medium)s
        :stop media input:
    :stop geometry:

:stop geometry definition:
```

When generating all input files from a template using the `egs-rollout` python script, the format placeholder `%(medium)s` is replaced with the medium for each simulation.

## 4. Materials

Materials are defined via [density effect correction files](https://github.com/nrc-cnrc/EGSnrc/tree/master/HEN_HOUSE/pegs4/density_corrections) bundled with the EGSnrc software. For reference, below is a table of the material composition and properties. Note that these figures are extracted directly from the EGSnrc density correction files, without any regard to precision or significant digits.

| Material | Elements (mass fractions)                             | I-value (eV) | Density        |
| -------- | ----------------------------------------------------- | ------------ | -------------- |
| Hydrogen | H (100%)                                              | 19.200001    | 8.37479965E-05 |
| Carbon   | C (100%)                                              | 78.000000    | 1.7000000      |
| Aluminum | Al (100%)                                             | 166.00000    | 2.6989000      |
| Cobalt   | Co (100%)                                             | 297.00000    | 8.8999996      |
| Silver   | Ag (100%)                                             | 470.00000    | 10.500000      |
| Tungsten | W (100%)                                              | 727.00000    | 19.299999      |
| Lead     | Pb (100%)                                             | 823.00000    | 11.350000      |
| Air      | C (0.0124%), N (75.5267%), O (23.1781%), Ar (1.2827%) | 85.666000    | 1.20478997E-03 |
| Water    | H (11.1894%), O (88.8106%)                            | 78.00000     | 0.998000       |

Below is the material definition block, identical in all EGSnrc input files in this comparison.

```ruby
:start media definition:

    :start air:
        density correction file = air_dry_nearsealevel
    :stop air

    :start water:
        density correction file = water_icru90
    :stop water:

    :start hydrogen:
        density correction file = carbon_graphite_1.700g_cm3
    :stop hydrogen:

    :start aluminum:
        density correction file = aluminum
    :stop aluminum:

    :start cobalt:
        density correction file = cobalt
    :stop cobalt:

    :start silver:
        density correction file = silver
    :stop silver:

    :start tungsten:
        density correction file = tungsten
    :stop tungsten:

    :start lead:
        density correction file = lead
    :stop lead:

:stop media definition:
```

## 5. Source

The source of particles is located at the origin, and isotropic on the unit sphere. Here is the template source input block that is used to generate all simulation input files for EGSnrc simulations in this comparison:

```ruby
:start source definition:
:stop source definition:
```

## 6. Scoring

Scoring is carried out using the EGSnrc ausgab object `dose_scoring_object`. While the volume of the egs_space scoring region is unbounded, its mass is arbitrarily set to unity to allow the dose scoring object to work as expected, computing a (fictitious) dose. This comparison tracks the total energy deposited, which is output by the `dose_scoring_object`. Here is a sample output showing the relevant energy deposited by incident particle.

```text

```

## 7. Parameters

The physical parameters are the same for all simulations, and are the default values in EGSnrc. As such they are not specified in the input. For reference, here is the listing of the Monte Carlo parameters output from a sample run:

```text

```

## 8. Results
