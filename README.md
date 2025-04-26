# Keep It Simple: Why Basic Investment Strategies Might Be Your Best Bet

## Description

This project investigates the effectiveness of basic and more advanced investment strategies. Using historical S&P 500 data from 2000 to 2025, I compare three approaches:

- **Dollar‑Cost Averaging (DCA)**
- **Simple Moving Average (SMA) Crossover**
- **'Buy the Dip' Strategy**

The analysis is presented in a Jupyter Notebook, supported by a blog post linked in `blog.txt`.

The full blog post can also be found [here](https://hackmd.io/@Nxl8pSr_RpOiZLTYH4Uunw/H1EyJQ4Rkx).

## Files:

- `Empirical Project.ipynb` – Main Jupyter Notebook with code, analysis, and commentary.
- `blog.txt` – Contains the URL to the online blog post.
- `README.md` – Instructions for replicating this project.

## How to Reproduce:

1. Open `Empirical Project.ipynb` using Jupyter Notebook 
2. Run all cells sequentially to reproduce the analysis and visualisations.

## Requirements:

- Python 3.10+
- Libraries:
  - pandas
  - numpy
  - matplotlib
  - yfinance
  
## Additional Information:

- Git version control was used throughout the project.
- All data was retrieved using `yfinance`  for the S&P 500 (`^GSPC`).
- You can swap the ticker symbol in the notebook to analyse any  stock of your choice.




## Code Overview

- **Data Acquisition**  
  Uses `yfinance` to download historical S&P 500 (`^GSPC`) data from 2000-01-01 to 2025-01-01.  
  _(You can swap `^GSPC` for any ticker.)_

- **Dollar-Cost Averaging (DCA)**  
  Invests $1,000 t each month on a randomly selected trading day and tracks cumulative shares, invested capital, and portfolio value over time.

- **Buy-the-Dip Strategy**  
  1. **Calculate Relative Close**  
     Compute how close the close is to the low as a percent of the daily high–low range.  
  2. **Flag Price Dips**  
     Mark days when the close sits in the bottom 25% of its range.  
  3. **Count Consecutive Dips**  
     Build a streak counter to identify back-to-back dips.  
  4. **Generate Buy Signal**  
     On the day _after_ two consecutive dips, flag a buy at that day’s open.  
  5. **Execute & Backtest**  
     For each buy signal:  
     - Invest $1,000 (or remaining cash) at the open  
     - Update cash balance and share holdings  
     - Record end-of-day equity using that day’s close  
  6. **Output**  
     Produce a table of trades showing Investment, Cumulative Shares, Cash Balance, and Portfolio Value.

- **SMA Crossover Strategy**

	1. **Calculate Moving Averages**  
	   Compute the 50-day and 200-day simple moving averages of the closing price.

	2. **Generate Crossing Signals**  
	   - Set `Signal = 1` when SMA_50 > SMA_200 (golden cross → go long)  
	   - Set `Signal = -1` when SMA_50 < SMA_200 (death cross → go short)

	3. **Detect Signal Changes**  
	   Identify dates where the `Signal` value changes from the previous day.

	4. **Build Trade List**  
	   For each crossing date:  
	   - If `Signal == 1`, record a “long” entry  
	   - If `Signal == -1`, record a “short” entry  

	5. **Backtest Loop**  
	   For each trading pair:  
	   - Calculate entry and exit prices from the `Close` series  
	   - Compute return:  
	     - Long: `(exit_price - entry_price) / entry_price`  
	     - Short: `(entry_price - exit_price) / entry_price`  
	   - Update `balance += balance * return_pct`  
	   - Record exit date, position, prices, return %, and new balance

	6. **Output Trades DataFrame**  


## GitHub Repository

View the complete project code and commit history here:  
https://github.com/MrChicken90/empirical-project


## Contact

For questions or feedback, please open an issue on GitHub or email me at `<kheelan90@gmail.com>`.


