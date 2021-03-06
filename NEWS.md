# scales 0.5.0.9000

# scales 0.5.0

* New function `regular_minor_breaks()` calculates minor breaks as a property
  of the transformation (@karawoo).

* Adds `viridis_pal()` for creating palettes with color maps from the
  viridisLite package (@karawoo).

* Switched from reference classes to R6 (#96).

* `rescale()` and `rescale_mid()` are now S3 generics, and work with `numeric`,
  `Date`, `POSIXct`, `POSIXlt` and `bit64::integer64` objects (@zeehio, #74).

# scales 0.4.1

* `extended_breaks()` no longer fails on pathological inputs

* New `hms_trans()` for transforming hms time vectors.

* `train_discrete()` gets a new `na.rm` argument which controls whether
  `NA`s are preserved or dropped.

# scales 0.4.0

* Switched from `NEWS` to `NEWS.md`

* `manual_pal()` produces a warning if n is greater than the number of values 
  in the palette (@jrnold, #68).

* `precision(0)` now returns 1, which means `percent(0)` now returns 0% (#50).

* `scale_continuous()` uses a more correct check for numeric values.

* NaN is correctly recognised as a missing value by the gradient palettes
  (ggplot2#1482).
  
# scales 0.3.0

* `rescale()` preserves missing values in input when the range of `x` is
  (effectively) 0 (ggplot2#985).

* Continuous colour palettes now use `colour_ramp()` instead of `colorRamp()`.
  This only supports interpolation in Lab colour space, but is hundreds of
  times faster.

# scales 0.2.5

## Improved formatting functions

* `date_format()` gains an option to specify time zone (#51).

* `dollar_format()` is now more flexible and can add either prefixes or suffixes
  for different currencies (#53). It gains a `negative_parens` argument
  to show negative values as `($100)` and now passes missing values through
  unchanged (#40, @dougmitarotonda).

* New `ordinal_format()` generates ordinal numbers (1st, 2nd etc)
  (@aaronwolen, #55)

* New `unit_format()` makes it easier to add units to labels, optionally
  scaling (@ThierryO, 46)

* New `wrap_format()` function to wrap character vectors to a desired width.
  (@jimhester, #37).

## New colour scaling functions

* New color scaling functions `col_numeric()`, `col_bin()`, `col_quantile()`,
  and `col_factor()`. These functions provide concise ways to map continuous or
  categorical values to color spectra.

* New `colour_ramp()` function for performing color interpolation in the CIELAB
  color space (like `grDevices::colorRamp(space = 'Lab')`, but much faster).

## Other bug fixes and minor improvements

* `boxcox_trans()` returns correct value when p is close to zero (#31).

* `dollar()` and `percent()` both correctly return a zero length string
  for zero length input (@BrianDiggs, #35)

* `brewer_pal()` gains a `direction` argument to easily invert the order
  of colours (@jiho, #36).

* `show_col()` has additional options to showcase colors better (@jiho, #52)

* Relaxed tolerance in `zero_range()` to `.Machine$double.eps * 1000` (#33).

# scales 0.2.4

* Eliminate stringr dependency.

* Fix outstanding errors in R CMD check

# scales 0.2.3

* `floor_time` calls `to_time`, but that function was moved into a function
  so it was no longer available in the scales namespace. Now `floor_time`
  has its own copy of that function. (Thanks to Stefan Novak)

* Color palettes generated by `brewer_pal` no longer give warnings when fewer
  than 3 colors are requested. (Winston Chang)

* `abs_area and `rescale_max` functions have been added, for scaling the area
  of points to be proportional to their value. These are used by
  `scale_size_area` in ggplot2.

# scales 0.2.2

* `zero_range` has improved behaviour thanks to Brian Diggs.

* `brewer_pal` complains if you give it an incorrect palette type. (Fixes #15,
  thanks to Jean-Olivier Irisson)

* `shape_pal` warns if asked for more than 6 values. (Fixes #16, thanks to
  Jean-Olivier Irisson)

* `time_trans` gains an optional argument `tz` to specify the time zone to use
  for the times.  If not specified, it will be guess from the first input with
  a non-null time zone.

* `date_trans` and `time_trans` now check that their inputs are of the correct
   type.  This prevents ggplot2 scales from silently giving incorrect outputs
   when given incorrect inputs.

* Change the default breaks algorithm for `cbreaks()` and `trans_new()`.
  Previously it was `pretty_breaks()`, and now it's `extended_breaks()`,
  which uses the `extended()` algorithm from the labeling package.

* fixed namespace problem with `fullseq`

# scales 0.2.1

* `suppressWarnings` from `train_continuous` so zero-row or all infinite data
  frames don't potentially cause problems.

* check for zero-length colour in `gradient_n_pal`

* added `extended_breaks` which implements an extension to Wilkinson's
  labelling approach, as implemented in the `labeling` package.  This should
  generally produce nicer breaks than `pretty_breaks`.

* `alpha` can now preserve existing alpha values if `alpha` is missing.

* `log_breaks` always gives breaks evenly spaced on the log scale, never
  evenly spaced on the data scale. This will result in really bad breaks for
  some ranges (e.g 0.5-0.6), but you probably shouldn't be using log scales in
  that situation anyway.

# scales 0.2.0

* `censor` and `squish` gain `only.finite` argument and default to operating
  only on finite values. This is needed for ggplot2, and reflects the use of
  Inf and -Inf as special values.

* `bounds` functions now `force` evaluation of range to avoid bug with S3
  method dispatch inside primitive functions (e.g. `[`)

* Simplified algorithm for `discrete_range` that is robust to
  `stringsAsFactors` global option.  Now, the order of a factor will only be
  preserved if the full factor is the first object seen, and all subsequent
  inputs are subsets of the levels of the original factor.

* `scientific` ensures output is always in scientific format and off the
  specified number of significant digits. `comma` ensures output is never in
  scientific format. (Fixes #7)

* Another tweak to `zero_range` to better detect when a range has zero length.
  (Fixes #6)
