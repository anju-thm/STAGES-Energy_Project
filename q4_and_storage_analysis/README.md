German Energy System Analysis (STAGES Project)

A marimo reactive notebook that pulls, cleans and analyzes German electricity generation, demand, trade, storage and weather data for 2025. It is the data pipeline behind the thesis chapters on the Q4 2025 electricity balance, storage infrastructure, expansion scenarios, cost analysis and renewable self-sufficiency.

What it does
Loads hourly German electricity generation, demand/consumption and cross-border trade data from SMARD (2025-01-01 to 2026-01-01).
Builds the Q4 2025 electricity balance: demand vs. domestic generation, renewable share, monthly breakdown (Oct/Nov/Dec), and net import/export totals.
Loads existing battery storage capacity from a local MaStR (Marktstammdatenregister) database — by federal state and by application category.
Runs storage expansion scenarios (+10 to +300 GWh), quantifying the reduction in net exports/imports and the resulting avoided import cost.
Calculates the Levelized Cost of Storage (LCOS) for Li-ion LFP batteries using IRENA Cost-of-Service Tool v2.0 best-case parameters, and compares annualized storage cost against import savings.
Builds renewable self-reliance scenarios: how much additional renewable capacity and storage would be needed to cover demand from renewables alone (EEG 2030 targets and two hypothetical scenarios).
Loads DWD weather data (wind speed, solar radiation, temperature, humidity) from multiple stations and correlates it with renewable generation (e.g. solar output vs. radiation and temperature).
Saves key figures to figures

Files this notebook expects alongside it (not included here)
utils.py — must define load_smard_series() and load_smard_market_trade(). The notebook imports both at the top; it will not run without this module.
data/mastr_storage_aggregated.db — a SQLite database with battery_summary and battery_by_state tables, used for the existing storage-infrastructure section. The notebook raises FileNotFoundError if it isn't found at data/mastr_storage_aggregated.db relative to the script.

Structure
Section	What it covers
Loading SMARD generation data	Hourly generation by source (renewable + conventional), Jan 2025–Jan 2026
Visualization of generation	Interactive time series, renewables and conventional sources separately
Loading SMARD consumption/load	Hourly demand, incl. pumped-storage consumption
Demand vs. generation comparison	Merges generation and demand into one table
Monthly renewable energy balance	Q4 2025 monthly balance (demand, generation, renewable share, net import proxy)
Export/import trade balance	Hourly net trade, by country, Q4 totals, year totals
Existing storage infrastructure (MaStR)	Battery capacity by federal state and application category
Storage expansion scenarios	+10 to +300 GWh: reduction in exports/imports, avoided import cost
Storage cost analysis (LCOS)	IRENA Li-ion LFP best case: cost per scenario vs. import savings
Renewable self-reliance scenarios	Capacity + storage needed to meet demand from renewables alone
DWD solar radiation	Per-station and multi-station radiation data, normalized vs. solar generation
DWD wind and temperature	Multi-station wind speed and temperature/humidity, correlated with generation
