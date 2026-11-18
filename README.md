# Transit timing pipeline: WASP-18 b and WASP-12 b

Author: Sana Sadiq

## What this project does
I measured the mid-time of every transit of two hot Jupiters in public TESS data, plotted an O-C (observed minus calculated) diagram, and tested whether each planet's orbital period is changing.

## Data
NASA TESS, SPOC 2-minute cadence, accessed with Lightkurve.
- WASP-18 b: 10 sectors (2, 3, 29, 30, 69, 96, 103, 104, 105, 106)
- WASP-12 b: 6 sectors (20, 43, 44, 45, 71, 72)

## Method
1. Download each sector and find the period and transit time with BLS.
2. Flatten the light curve while protecting the transits.
3. Remove bad transits.
4. Fit one transit shape (batman model, least squares).
5. Fit the mid-time of each transit with that shape held fixed.
6. Fit a straight line and a curved (quadratic) model to the mid-times and compare them with BIC.

All steps are in one function, `analyze()`.

## Results
**WASP-18 b:** 213 transits used (8 of 226 removed). Period = 0.94145236 d. dP/dt = -2.5 +/- 1.1 ms/yr. The straight line and the curve have the same BIC (221.7 vs 221.7), so I find no significant period change.

**WASP-12 b (validation):** 118 transits from 6 sectors. dP/dt = -21.6 +/- 13.8 ms/yr. The sign matches the decay expected for this planet, but the significance is low with TESS data alone.

I also ran an injection-recovery test on the WASP-18 b timings: decays of 0, -3, -6, -12 and -29 ms/yr were injected and recovered by the pipeline.

## Limitations
- The transit shape is fitted once and kept fixed for all transits.
- Limb darkening is fixed, not fitted.
- TESS covers a limited time span, so small period changes are hard to detect.

## Files
- `Transit_timing_pipeline.ipynb`: full code and outputs
- `WASP-18_times.csv`, `WASP-12_times.csv`: measured transit mid-times
- `Transit_timing_pipeline.pdf`: PDF copy of the notebook
