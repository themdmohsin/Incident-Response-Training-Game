[![Built with askThili](https://msrit.ask.thili.ai/api/v1/public/projects/3ww6qma7b4/badge.svg)](https://msrit.ask.thili.ai/b/3ww6qma7b4)
# Incident Response Training Game

Play a three-round fictional dispatch exercise. Read the incident history, inspect the model's top three forecasts, predict the next event, and commit up to two different units before the report is revealed. Each dispatch consumes one unit from the scenario's finite stock.

## Run locally

From the project directory with Python 3.12:

```powershell
python -m app.cli hello
python -m app.cli play --scenario underpass
python -m app.cli patterns
python -m unittest discover -s tests -v
```

Run play without a scenario to draw one at random. Replay underpass, junction or waterfront to compare decisions. No keys, network or installation required.

## Score

A correct prediction earns four points. Covering the observed event earns another four. Each unnecessary dispatch costs one. Passing uses zero units. The final report also shows prediction accuracy, coverage and the share of dispatched units that were useful.

## Data and model

app/reports.py contains six base sequences, twelve local training reports and three separate playable drills. These synthetic events and unit assignments are game rules. The directed-pattern command represents each adjacent pair as a basket tagged with source and target positions. Support is the fraction of all training transitions containing that directed pair.

app/model.py trains a small softmax language model on the base sequences, then continues updating the same weights on local reports. The model learns next-event likelihoods from the most recent event, the previous pair and a shared bias. Training is deterministic and runs on startup. The forecast percentages describe the toy model's distribution.

## Attribution

The bundled Apriori miner comes from thili-ai/thilimarketbasket under the MIT license. Its bitset construction uses Python integers to keep the game dependency-free. See thilimarketbasket/LICENSE and https://github.com/thili-ai/thilimarketbasket.

