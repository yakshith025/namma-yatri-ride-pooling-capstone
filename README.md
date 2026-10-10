# Namma Yatri Ride Pooling: NY Share and NY Pool

Two ride-sharing matching algorithms for the **Namma Yatri** platform in Bengaluru, built on Uber's H3 hexagonal index and evaluated on more than 1.6 million real rides. Batched rides saved up to **~40% of distance** and **12.6 t of CO₂**.

## The two algorithms

- **NY Share (pre-dispatch batching):** groups compatible requests (nearby pickups and drop-offs) before dispatch. The waiting window is dynamic, 3–8 minutes, and adapts to trip distance, time of day, local demand density and driver supply (ETA).
- **NY Pool (en-route dynamic pooling):** a sweep-line streaming algorithm matches new requests to rides already in progress. It uses a temporal priority queue, a spatial inverted index and a hierarchical filter chain: bearing → trajectory similarity → road-network detour check, capped at 30% detour.

## Results

| Metric | NY Share | NY Pool |
|---|---|---|
| Rides evaluated | 1,657,148 (14 days) | 138,654 (2 Aug 2025) |
| Rides batched | 3.41% / 4.16% / 5.62% (base wait 3 / 5 / 7 min) | 27.08% |
| Distance (VKT) saved | 39.93% of batched-ride distance | 15.84% |
| CO₂ saved | 12,568 kg | 5,492 kg |

## Repository structure

```
code/
├── ny_share_batching.ipynb         NY Share: dynamic-window batching
└── ny_pool_dynamic_pooling.ipynb   NY Pool: streaming en-route matcher
report/final_report.pdf             full capstone report
```

## Data

The trip data belongs to Namma Yatri and is **not included** in this repository. To run the notebooks on your own data, put the parquet trip files next to the notebooks, or change `FILE_PATH` / the glob pattern at the top of each notebook.

## Getting started

```bash
pip install -r requirements.txt
cd code
jupyter notebook
```

NY Pool's detour check calls an [OSRM](https://project-osrm.org/) routing server at `http://127.0.0.1:5000`. Run OSRM locally with a Bengaluru / South India OpenStreetMap extract, or change the URL in the notebook.

## Team

M.Tech Capstone, CiSTUP, Indian Institute of Science (IISc), Bengaluru, 2026. Supervisor: Prof. Vijay Kovvali.
Yakshith Maddineni, Vidhi Sonkar, Anant Rajput, Rahul Dev Sharma, Ashish Kumar Verma.
