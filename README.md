# StockPiceMovement_202401100400201
Stock Price Movement Analysis

Overview

This project analyzes stock price movements using Python. It fetches historical stock data, calculates a moving average, and visualizes stock trends. The data is retrieved using the yfinance library, processed with pandas, and plotted with matplotlib.

Features

Fetches stock price data from Yahoo Finance

Computes a moving average for better trend analysis

Plots closing prices and moving averages on a graph

Handles cases where stock data is unavailable

Prerequisites

Ensure you have Python installed along with the following libraries:

pip install yfinance matplotlib pandas

Usage

Run the following script to fetch and visualize stock price data:

import yfinance as yf
import matplotlib.pyplot as plt
import pandas as pd

# Function to fetch and plot stock data
def plot_stock_movement(stock_symbol, start_date, end_date, ma_window=5):
    # Fetch historical data
    stock_data = yf.download(stock_symbol, start=start_date, end=end_date, interval="1d")

    if stock_data.empty:
        print("No data found for the given stock symbol and date range.")
        return

    # Calculate moving average
    stock_data['MA'] = stock_data['Close'].rolling(window=ma_window).mean()

    # Plot closing price and moving average
    plt.figure(figsize=(12, 6))
    plt.plot(stock_data.index, stock_data['Close'], label='Close Price', color='blue')
    plt.plot(stock_data.index, stock_data['MA'], label=f'{ma_window}-Day Moving Avg', color='red', linestyle='dashed')

    plt.xlabel('Date')
    plt.ylabel('Stock Price')
    plt.title(f'{stock_symbol} Stock Price Movement')
    plt.legend()
    plt.grid()
    plt.show()

# Example usage
stock_symbol = "AAPL"  # Change this to your preferred stock symbol
start_date = "2024-02-01"
end_date = "2024-03-01"
plot_stock_movement(stock_symbol, start_date, end_date)

Expected Output

A graph displaying the stock's closing price and its moving average over the selected period.

Future Enhancements

Add more moving averages (e.g., 10-day, 50-day) for better analysis.

Fetch and analyze stock data for multiple companies.

Include additional financial indicators like RSI and Bollinger Bands.
