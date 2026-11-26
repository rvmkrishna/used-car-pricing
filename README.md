# What drives the asking price of a used car?

**Dealer inventory briefing · Berkeley Practical Application 11.1**

Start each appraisal with vehicles of a similar model year and mileage, then narrow the comparison by make and model. Age and mileage were the strongest predictors of advertised price. Shuffling age alone raised the model’s average dollar error by about $4,567. Shuffling mileage raised it by $2,153. Make and model each added roughly $1,000 of error when shuffled separately.

[Open the executed CRISP-DM notebook](used_car_pricing.ipynb)

## Pricing and buying decisions

| Dealer decision | What the listings show | How to use it |
|---|---|---|
| Which listings make good comparisons? | After adjusting for recorded specifications, the linear model associated each additional year of age with a $1,214 lower ask and each additional 10,000 miles with a $593 lower ask. | Match model year and mileage first. Check nearby examples of the same model before quoting a trade-in. These are average associations across the selected inventory. |
| How much more capital does a pickup require? | Median training-set asks were $23,999 for pickups, $13,499 for SUVs and $9,000 for sedans. | The $14,999 pickup–sedan gap narrowed to $3,523 in the additive model after adjustment. Budget separately by body style. Confirm that local sale proceeds, time on lot and reconditioning costs support the extra capital before increasing pickup purchases. |
| When does an estimate need review? | The best model missed held-out asking prices by $3,113 on average. Larger misses pushed RMSE to $5,211. | When expected gross profit is close to the typical pricing error, have an appraiser review comparable listings, trim, condition and repair costs before setting the bid. |

## How accurate was the estimate?

| Model | Three-fold validation MAE | Held-out MAE | Held-out RMSE |
|---|---:|---:|---:|
| Median asking price | $9,557 | $9,465 | $13,706 |
| Ridge regression | $4,797 | $4,443 | $6,749 |
| Gradient-boosted trees | $3,302 | $3,113 | $5,211 |

The tree model reduced average absolute error by 67% against the median benchmark across 39,251 held-out listings. The estimated improvement was $6,352 per listing, with a paired bootstrap 95% interval of $6,280–$6,445. The interval summarizes variation within this historical test sample. The $3,113 MAE is an average across vehicles, so an individual appraisal can miss by considerably more.

## Coverage and next steps

The course file contains 426,880 listings. Price, year and mileage filters retained 350,613. Removing repeated VINs and indistinguishable within-state profiles left 196,255. Classic, low-price, high-mileage and specialty vehicles fall outside the study’s scope. Missing condition and inconsistent model descriptions limit the precision of individual estimates. The random test split measures performance on similar historical listings.

Pilot the estimate on recent local appraisals. Record asking price, final sale price, acquisition cost, reconditioning spend and days on lot. Compare error and gross profit by body style and price tier before changing purchasing targets. A listing premium can coexist with slow turnover or a thin margin.

## Reproduce the analysis

1. Download the [course starter archive](https://mo-pcco.s3.us-east-1.amazonaws.com/BH-PCMLAI-R2/module11/practical_application_II_starter.zip) and extract `data/vehicles.csv` into this repository’s `data` folder.
2. In Python 3.13, install the dependencies with `python -m pip install -r requirements.txt`.
3. Start `jupyter lab` from the repository root, open the notebook and run all cells in order. All splits, samples and bootstrap draws use a fixed seed.

The notebook follows the six phases described in the [course CRISP-DM reading](https://mo-pcco.s3.us-east-1.amazonaws.com/BH-PCMLAI-R2/module11/readings_starter.zip).
