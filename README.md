# Sentiment Analysis Based Trading Approach
This project was conducted as an analysis and feasability study on the use of sentiment analysis when developing an investment strategy. Our hypothesis entering this project was that by following common sentiment, as gathered from tweets posted on a certain day, we can determine which trades are most likely to become profitable in the near future. 

## Background
Our model uses a pretrained natural language processing model called [tweetnlp](https://github.com/cardiffnlp/tweetnlp) to analyze the sentiment of the tweets. We gathered tweets under certain hashtags, deeming them most likely to mention specific equities and discussing topics relevant to our model, and extracted the trade symbols within them. Our model then determines which trade is most likely to see a large move in the near future from a variety of metrics, including total sentiment and number of mentions. 

Our model was tested over about a year of backtesting, finding about 38% in total returns, which was over double the total return of the S&P500 during the same time period. The strategy we implemented was very simple, holding up to 10 equities at a time, and replacing the longest held one on each day (so typically holding each stock a total of 10 trading days). We chose to do so with the prediction that tweets tended to focus on stocks with short term volatility (and thus, short term upside) rather than long term investment potential.

## Quickstart
Feel free to copy any of our notebooks provided in the repo for personal analysis, although we do not take responsibility for any losses/gains induced on personal trading. The dependencies are installed automatically in CoLab, though may need to be installed manually if used locally. 

Change the line 

```
os.chdir("drive/MyDrive/sentiment_bot")
```

in the `./model.ipynb` and `./analysis.ipynb` to the directory containing the dataset you plan on using. Also change the actual filename of the dataset, located in `./model.ipynb` at 

```
tweets = pd.read_csv('stock.csv', on_bad_lines='skip')
```

Ensure that your dataset is a csv containing the columns `tickers_mentioned`, `timestamp`, and `tweet_text`; otherwise, additional editing in `./model.ipynb` should be done to ensure proper data reading. Any additional data processing can be done by editing the cell currently containing 

```
tweets = tweets.dropna()
tweets = tweets[tweets['category']=='stock_images']
tweets = tweets.drop(columns=['tweet_url', 'tweet_type', 'price_of_ticker', 'change_of_ticker', 'category'])
```

After necessary changes have been completed, you can run `./model.ipynb`, either as a Python script or in a Jupyter Notebook environment. Doing so will save the results of the trades labeled `./trades.XXXXXXXXX`, where the last characters are the current timestamp. This can be viewed, loaded, and analyzed by running the necessary cells in `./analysis.ipynb`.

## Contributions
Special thanks to [Hayun Jung](https://github.com/Yun505) for her help in developing the model and performing analysis. Any contributions or usages are welcome!
