# BA 545 Course Project 1: Advanced Preparation of Financial Data
## Spring 2020

## Overview of the Competition

Understanding pricing strategies in the context of the Initial Public Offering (IPO) process has been receiving much attention. Most prior studies have however focused on information sources from post issuance periods, and understanding such strategies from the management’s perspective during the IPO process is still an open research issue. Form 424 variants, as finalized IPO prospectus approved by Security Exchange Committee (SEC), contain rich and genuine information about the issuing firms. In this study, we analyze the inter-relationships between the management’s confidence (through the proxy of sentiments expressed in textual contents in the Management’s Discussion & Analysis (MD&A) sections in the prospectus) and the pre-/post-IPO valuations.

The data used for this project includes successful U.S. IPOs from more than 600 companies. Our "client" is interested in which features are most important to the "underpricing" phenomenon most commenly seen in the stock market. By using advanced and novel methods to prepare the collected IPO data, we will break down the data in order to process it through phases of a CRISP-DM model. Through this project our team experimented with many different pipelines and methods. We would like to briefly outline 2 pipelines that produced the best results after running our classification model. 

We would like to briefly outline 2 pipelines that produced the best results. 

Our project pipeline number 1 is as follows:
- Descriptive
- Imputation
- Feature engeneering (Calcuation)
- Normalization  
- Outlier Detection (3-standard deviations)
- Standardization (z-score, scaler...)
- Correlation analysis
- Recoding (one-hot encoding, binning)
- Feature Selection

Our project pipeline number 2 is as follows:
- Descriptive
- Imputation
- Feature engeneering (Calcuation)
- Outlier Detection (IQR)
- Standardization (min-max)
- Normalization
- Correlation analysis 
- Recoding (encoding, binning)
- Feature selection

## Data Dictionary 
**IPO pricing used to derive targets:*
- P(IPO): Final offering price P(IPO)
- P(H): Filling price range higher bound 
- P(L): Filling price range lower bound 
- P(1Day): First day trading price 

**IPO Characteristics - Economic/Accounting/Financial Determinants:**
- C1: Days between the innitial S-1 filling and form 424B4 
- C2: If leading underwriter has a higher rating than 8, dummy variable set to 1 otherwise 0
- C3: Trailling EPS
- C4: Prior Nasdaq 15-day returns 
- C5: Outstanding shares 
- C6: Offering shares
- C7: Trailling annual firm sales 

**Textual Characteristics of IPO prospectus MD&A section:**
- T1: Number of sentences 
- T2: Number of words
- T3: Number of real words
- T4: Number of long sentences 
- T5: Number of long words

**Sentimental Characteristics of IPO prospectus MD&A section:**
- S1: Number of positive words
- S2: Number of negative words
- S3: Number of uncertain words

**Targer Variables:**
- Y1: Pre-IPO pricing revision
- Y2: Post-IPO innitial return

**Control Variables:**
- C3prime: If EPS positive at the time of the IPO set to 1 otherwise 0
- C5prime: Share overhang
- C6prime: Up revision

**IPO Identifier:**
- I1: Ticker
- I2: Company name
- I3: Standard Industry Classifier 

## Data assumptions

**IPO characteristics (C columns)** can contain 0, less than 0 values but no strings<br>
That is because finance/accounting determinants can be 0 or be negative (e.g. EPS, sales, can be negative and 0)<br>

**Sentiment characteristics (S columns)** can contain 0 values but cannot be less than 0 or have strings<br>
Our assumption is that you cannot have a negative amount of words (we only encountered 2). We decided we will allow 0 values here because there aren't many. Our reasoning this section to contain 0 values is becasue of the difficulty translating sentimental analysis for companies not in the US and lack of data. <br>

**Textual Characteristics (T3-T5 columns )** can contain 0 and less than 0 values but no strings, however, **T1 and T2** (Nbr of sentences, number of words respectively) cannot contain 0, less than 0, and no string values. Our assumption is the same that you simply cannot have a negative or zero amount of words. <br>

**IPO pricing (P columns)** cannot contain 0, less than 0, and string values <br>
This column cannot contain these values because we will use it to calculate the control and target variables. <br>
    
**Note:** These calculations will make P columns are called force predictors or price leakers, therefore, they will have to be removed because they will interfere with results (e.g. it can happen that you get 100% accuracy by including them which is unrealistic). 