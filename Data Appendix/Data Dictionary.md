# ![](https://ga-dash.s3.amazonaws.com/production/assets/logo-9f88ae6c9c3871690e33280fcf557f33.png) Data Dictionary

To get a better understanding of labee names it is recommended to read the [Finance Key Concepts file.](https://github.com/berkurka/Mutual_Fund_Clustering/blob/master/Data%20Appendix/Finance%20Key%20Concepts.md)


|Label|Type|Description|
|---|---|---|
|Name|String|Fund Name|
|CNPJ|String|Unique code per fund|
|ManagementFee|Float|Fee charged to pay for management costs.|
|MinimumInvestment|Integer|Minimum investment accepted by the fund in Brazilian Real.|
|PerformanceFee|Float|Fee charged if fund returns exceed its benchmark's|
|PortfolioManager|String|Name of primary fund manager|
|redemption_delay|Integer|Number of days after redemption order the fund will take to transfer back money to investors acount.|
|age_months|Integer|Number of months since fund's start date.|
|CVMCategory_FixedIncome|Integer|1 if fund category is Fixed income, 0 otherwise|
|CVMCategory_Multimarket|Integer|1 if fund category is Balanced, 0 otherwise|
|CVMCategory_Equities|Integer|1 if fund category is Equity, 0 otherwise|
|CVMCategory_FX|Integer|1 if fund category is Currency, 0 otherwise|
|TaxClassification_Exempt|Integer|1 if fund exempt from income tax, 0 otherwise|
|TaxClassification_LongTerm|Integer|1 if the fund has long term income tax rates, 0 otherwise|
|TaxClassification_ShortTerm|Integer|1 if the fund has short term income tax rates, 0 otherwise|
|PrivateCreditAnbima_Yes|Integer|1 if the fund invests 50% or more in private bonds, 0 otherwise.|
|PrivateCreditAnbima_Notapplicable|Integer|1 if the fund is not eligible for this classification , 0 otherwise.|
|LeveragedAnbima_Yes|Integer|1 if the fund is authorized to make leveraged operations. |
|PerformanceFeeReferenceIndex_100%doIBX|Integer|1 if performance reference index equals 100 IBX, 0 otherwise|
|PerformanceFeeReferenceIndex_100%doIbovespa|Integer|1 if performance reference index equals 100 of Ibovespa, 0 otherwise|
|PerformanceFeeReferenceIndex_Other_performance_fee|Integer|1 if performance reference index is other, 0 otherwise|
|PerformanceFeeReferenceIndex_Thereisnot|Integer|1 if does not charge performance fee, 0 otherwise|
|Benchmark_Dollar|Integer|1 if fund benchmark is Dollar vs Brazilian Reals (USD/BRL), 0 otherwise|
|Benchmark_IBX|Integer|1 if fund benchmark is IBX, 0 otherwise|
|Benchmark_IMA-B|Integer|1 if fund benchmark is IMA-B, 0 otherwise|
|Benchmark_Ibovespa|Integer|1 if fund benchmark is Ibovespa, 0 otherwise|
|Benchmark_NotInformed|Integer|1 if fund benchmark is not informed, 0 otherwise|
|Benchmark_Other_Benchmark|Integer|1 if fund benchmark is another type, 0 otherwise|
|Last_Assets|Float|Fund most recent total asset under management|
|Assets_Flow_6m|Float|Fund net asset flow in last 6 months|
|Assets_Flow_12m|Float|Fund net asset flow in last 12 months|
|Assets_Flow_24m|Float|Fund net asset flow in last 24 months|
|Average_Assets_6m|Float|Average asset under management in the last 6 months.|
|Average_Assets_12m|Float|Average asset under management in the last 12 months.|
|Average_Assets_24m|Float|Average asset under management in the last 24 months.|
|Return_6m|Float|Fund return, over a 6 month period.|
|Return_12m|Float|Fund return, over a 12 month period.|
|Return_24m|Float|Fund return, over a 24 month period.|
|Volatility_6m|Float|Fund volatility, over a 6 month period.|
|Volatility_12m|Float|Fund volatility, over a 12 month period.|
|Volatility_24m|Float|Fund volatility, over a 24 month period.|
|Excess_Return_-_CDI_Opening_6m|Float|Return that exceeded CDI Benchmark, over 6 month period.|
|Excess_Return_-_CDI_Opening_12m|Float|Return that exceeded CDI Benchmark, over 12 month period.|
|Excess_Return_-_CDI_Opening_24m|Float|Return that exceeded CDI Benchmark, over 24 month period.|
|Excess_Return_-_Ibovespa_6m|Float|Return that exceeded Ibovespa Benchmark, over 6 month period.|
|Excess_Return_-_Ibovespa_12m|Float|Return that exceeded Ibovespa Benchmark, over 12 month period.|
|Excess_Return_-_Ibovespa_24m|Float|Return that exceeded Ibovespa Benchmark, over 24 month period.|
|Excess_Return_-_Dollar_6m|Float|Return that exceeded Dollar vs Brazilian Real (USD/BRL) Benchmark, over 6 month period.|
|Excess_Return_-_Dollar_12m|Float|Return that exceeded Dollar vs Brazilian Real (USD/BRL) Benchmark, over 12 month period.|
|Excess_Return_-_Dollar_24m|Float|Return that exceeded Dollar vs Brazilian Real (USD/BRL) Benchmark, over 24 month period.|
|#_Funds_managed|Integer|Count of how many different funds are managed by the same manager. Considering only funds within the sample.|
|Manager_avg_Assets|Float|Sum of assets under management for the fund manager. Considering only funds within the sample|
