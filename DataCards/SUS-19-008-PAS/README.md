### Unpacking

There are almost 2GB worth of cards, so due to github file size limitations,
they were compressed and split via
```bash
tar -czf limits_13March2019_PAS.tar.gz limits_13March2019_PAS/
split -b 99M -d limits_13March2019_PAS.tar.gz "limits_13March2019_PAS.tar.gz.part"
```
To uncompress, do
```bash
cat limits_13March2019_PAS.tar.gz.part* | tar -xz
```

### Running one card
To run on one mass point of T1tttt, do
```bash
( cd limits_13March2019_PAS ; combine -M AsymptoticLimits card_fs_t1tttt_m1850_m400_all_run2.txt )
```

### Card structure

* Each card is shape-based, so it links to rootfiles with nominal yields as well
as systematic variations. Yields are a sum over the 3 years.
* There are 5 channels in the card, resulting from
using `combineCards.py` on cards from different kinematic regions (HighHigh,
HighLow, LowLow, MultiLepton, LowMET).  
* If a nuisance name starts with `y2016_`, for example, it
affects the 2016 component of the yields. Nuisances without a year in the name
are correlated across the years.
* Nuisances like `TTH`, `TTWSF`, `TTZSF`, `WW`, `WZSF`, `XG`, `rares`, `flips` correspond
to the large normalization uncertainties taken on the corresponding process.
* Other (experimental) nuisances include `btaghf`, `btaglf`, `lumi`, `lep` (lepton efficiency),
`trig` (trigger efficiency), `jes`, `isr` (nISR reweighting/uncertainty),
 `prefire`, `met` (pf-gen MET systematic for fastsim)
* The four `fakes_normNB0`, ..., `fakes_normNB3` nuisances are 30% yield variations for the non-prompt lepton background, separated into 
bins of 0, 1, 2, and at least 3 b-tagged jets
