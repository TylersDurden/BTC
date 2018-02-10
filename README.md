# BTC 
This projects attempts to use Historic Price, Volume and Trading Data along with live 
Orderbook/Price data to make estimates on future prices. Continually adjusting to minimize 
the error of the prediction, with the help of more and more live orderbook data, the quality
of the predictions should become more precise. 

![30 Day Data](https://raw.githubusercontent.com/TylersDurden/BTC/master/ExampleFigure.png)


On the front end, this program uses 4 classes to collect, parse and organize live
market prices and orderbooks. 

On the Back end the program is using nearly 60k data points, from 6 different data sets
covering 10 active BTC markets, which includes hourly information about the last 30days
of Price, Volume and Trade-Per-Minute activity, and minute-by-minute data from the last 24 hours. 

![24 Hr Data](https://raw.githubusercontent.com/TylersDurden/BTC/master/30dMarketSummaryBfnx.png)


## CSVtoTXT 
This is useful because Python modules like Numpy work really well with .txt files
and are also very powerful for visualization and mathematical analysis. This class
will be used as the last bridge between java code and python code. From here, 
files generated by other classes and saved as CSVs will be converted and fed into 
the python applications. 

## DataCollector 
Grabs the Orderbook data for Bitfinex, and Bitstamp. Parses each orderbook into a
Map<TradeNumber,Vector<Price,Volume>>, where TradeNumber is an Integer and the 
coupled Price/Volume orders are Doubles. 

# DataTraining Layer  
Ultimately the goal is to use historic knowledge of the movement of these exchanges
to be able leverage orderbook data into predictions about imminent price movements. 
So before any live orderbook data can truly be processed, the data training layer
will first be trained with a large volume of historic data across many exchanges
over a long period of time. 

As the program runs, it begins to append the history of this price data, now taking
into account the orderbooks that created the resulting price changes, and includes 
this information by propogating it back through the most recent history to modify
orderbook weights and by extension next predictions. 

# Maya
Borrowed from Buddhist philosophy, Maya "are defined as aspects of the mind that 
apprehend the quality of an object". The Maya class is transferrable to all data sets,
but it takes their similar qualities, and applies them in ways that are useful for our
needs in a generic way (relative highs, lows, inflection points, derivs, etc.)


# Data Sets 
For the historic data sets, I've chosen to utilize CSVs found at data.bitcoinity.org. 
I would highly suggest anyone interested in Bitcoin visits their site, it's amazing. 


# Network 
Thus far the Network is made up of the DataTrainingLayer and the HistoricDataCollector. 
HistoricDataCollector is meant to take long term chart data and add what it finds to
Market objects. The DataTrainingLayer will be where historic and live data meet, are
combined and analyzed, and where the data is fed into a pattern recognition system
to try and find the real-time probabilities of impending market shifts based on a learned
understanding of Orderbook topology.

Orderbook is split apart from the rest of historic and live data in the DataTrainingLayer. 
From there it is dissected, with every trade being assigned a weight based on the current
price and the 24hr data. 

The Orderbook network is trained with BookKeeper, and ideally will be integrated with Points
(a class to assign the weight of each point based on the weight of the previous point), after
it has been trained with historic data, to use both past and present information to make
the most educated guesses possible about the (near)  future.  

# Predictive Techniques Employed 
The ultimate goal of this program is to utilize an articial network to take a vast amount 
of previoous bitcoin related data, in order to inform the program on how to make short term
price predictions based on the current orderbook of live exchanges topography. 

# Linear Regression 
Regression will be a key statistical tool for this project. It will be used to characterize
segments of data, compare segments of data, and to prepare predictions. Regression is simply
a mathematical tool to make approximate descriptions of, and interpretations about, the patterns
within a series of numbers.  

# Fourier Analysis 
Although I am unsure as to whether or not this will work, I am curious as to the efficacy 
of using a fourier series to analyze the combined swings of all the markets at once. Treating
each data set as an arbitrary function, and normalizing the range such that the function 
become a unitless oscillator with ouputs varying between -1 (and abslute minimum) and 1
(an absolute maximum), I believe the "little wiggles" and "larger wiggles" will be differentiated
and perhaps the program could estimate a universal function common to all of the waves combined? 
Totally a theory, not sure it would work.


# Demo Build - Watch to see how to run this project for yourself 
<a href="http://www.youtube.com/watch?feature=player_embedded&v=JLySP2X6L6g" target="_blank">
<img src="http://img.youtube.com/vi/JLySP2X6L6g/0.jpg" alt="Build and Run Demo" width="240" height="180" border="10" /></a>

