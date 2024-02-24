# Master-Thesis_Portfolio_Optimization_PCA


### Thesis Purpose

The main purpose of this thesis was to investigate if the Markowitz Mean-Variance Optimization (MVO) could be further improved when robustifying the estimation method chosen to calculate the required input parameters such as the covariance matrix. The Enhanced Portfolio Optimization (EPO) method is based on the paper published by Lasse Heje.

We sought to test various denoising methods including PCA, RMT and Shrinkage. Further methods could be explored such as Black-Litterman, Machine Learning Regularization such as Elastic Net or Allocation Weight Constraints.

Problem: Markowitz MVO is known to perform poorly in practice due to poor estimation choices such as sample approximates used as estimated returns and (co)variances, consequently constructing unjustified bets in a portfolio due to noise. 

Solution: We denoise the estimates using aforementioned methods, however being mindful that introducing further estimate methods might cause other estimation errors to occur, thus leaning towards relatively simple and quick algorithms or methods.

### Data

The thesis sought to solve a practical solution, thus a broad investment universe seemed necessary.
We use 2 datasets, one solely consisting of equities however used widely academically allowing us to compare results to previous academia, this dataset is retrieved from an API to Kenneth R. Frenchs website and the inherent datasets available. The "Global" dataset is consisting of equities, (government) bonds and commodities (futures) retrieved from a Bloomberg Terminal.

The equity dataset is the Fama French 5 Factor model (Mkt-Rf, SMB, HML, RMW, CMA) and their daily excess returns, as described in: https://mba.tuck.dartmouth.edu/pages/faculty/ken.french/Data_Library/f-f_5_factors_2x3.html

The global dataset is retrieved via a Bloomberg Terminal and consists of 47 different futures contracts written on equities, bonds and commodities. Furthermore we included 10 different 3M FX Forward contracts as a component as well. We used 3M US T-bill rate as risk free rate proxy.

### Estimation and Optimization 

##### Estimation
Estimation of expected returns were proxied by return signals, specifically Time Series Momentum and Cross Sectional Momentum to test the sensitivity of EPO towards return signals.

Estimation of covariance matrix and denoising hereof was done using various methods.
- Random Matrix Theory (RMT) 'cleans' a (covariance) matrix by the use of its eigenvalues and -vectors making it rotationally invariant and uses regularization to robustify through an algorithm.
- PCA is used to specify the directions containing the most variance (thus information) through linear combinations of the variables, allowing for dimensionality reduction i.e. removing the noisy variables distorting the MVO result.
- Shrinkage reduces the covariance matrix towards the identitiy matrix, essentially removing covariance structure as the shrinkage amounts increases, but the marginal benefit of shrinkage - even between 5-10% - are significant, while leaving the covariance structure pronounced.

##### Optimization
We optimized a range of portfolios all diverting in data, return signal, covariance estimate and optimization method.

Optimization Methods include the standard MVO, however also varied EPO solutions, which are alterations of the standard framework (MVO), specifically varying the input parameters as suggested above, and for some of the iterations even introducing an additional shrinkage parameter. 


### Findings

We found our EPO solution heavily outperformed the MVO solution, not exactly in a backtest, however the turnover of MVO made it often highly leveraged and utilizing extensive turnover to achieve its risk-adjusted returns. Thus in a practical sense the EPO solution moderated the necessary turnover of the optimization framework, however struggled to outperform the equally weighted and market portfolio when imposing moderate transaction costs and assessing in risk-adjusted terms.

We found the method applied well to all of the adjusted covariance inputs and return signals variants, suggesting a robust framework, however return signals does impact results noticeably.


