---
title       : Implied volatility and greeks
subtitle    : For European Options using Black-Scholes formula
author      : David K
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [mathjax]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
github:
      user: davidkvists
      repo: project
 

 
--- .class #id 
## Pricing European options with Black-Scholes
 > 1. Black-Scholes formula to price European call option
 $$C(S,t)=S e^{-q T}N(d_1)-Ke^{-r T}N(d_2)$$
 > 2. Black-scholes formula to price European put option
 $$P(S,t)=Ke^{-r T}N(-d_2)-S e^{-q T}N(-d_1)$$
 where
 $$d_1=\frac{log(\frac{S}{K})+(r-q+\frac{\sigma^2}{2})T}{\sigma \sqrt{T}}$$
 $$d_2=d_1-\sigma \sqrt{T}$$
 Inputs:
 <table>
    <tr>
        <td>S - asset price, K - strike price, T - time to maturity,  r - risk-free rate (annual rate expressed in continuous compunding), q - dividend yield, N() - cummulative distribution function of standard normal, $\sigma$ - volatility</td>
    </tr>
</table>

--- .class #id
## Implied volatility and Delta

 > 1. Implied volatility is a volatility parameter $\sigma_{imp}$ that entered in Black-Scholes formula as $\sigma$ gives the price of the option that equals its marketprice.
 Implied volatility represents the expected volatility of a stock over the life of the option.
 
 > 2. Delta measures sensitivity of the option price with respect to changes in the underlying price.   $$\Delta=\frac{\partial C}{\partial S}$$
 
 >   Delta for European call option is calculated as
      $$\Delta_{call}=N(d_1)$$
      
 >   Delta for European put option is calculated as
      $$\Delta_{put}=N(d_1)-1$$

---
## Gamma and Vega

  > 1. The rate of change for delta with respect to the underlying asset's price. Gamma is an    
       important measure of the convexity of a derivative's value, in relation to the 
       underlying. Gamma is the same for call and put.
       $$\Gamma=\frac{\partial^2 C}{\partial S^2}$$
       $$\Gamma=\frac{N^`(d_1)}{S\sigma \sqrt{T}}$$
  > 2. Vega is the measurement of an option's sensitivity to changes in the volatility of the 
       underlying asset. Vega is the same for call and put.
       $$Vega=\frac{\partial C}{\partial \sigma}$$
       $$Vega=S N^`(d_1) \sqrt{T}$$

---
## Rho and Theta
   1.  Rho measures sensitivity to the interest rate: it is the derivative of the option \   
         value with respect to the risk free interest rate. 
         $$Rho=\frac{\partial C}{\partial r}$$
   2. Rho measures the sensitivity of the value of the derivative to the passage of time:    
        the "time decay."
       The code for computing Theta of European call option is given below:
  

```r
rho_call<-function(S,T,K,r,s,q){
      d1<-(log(S/K)+(r-q+0.5*s^2)*T)/(s*sqrt(T))
      d2<-d1-s*sqrt(T)
      K*T*exp(-q*T)*pnorm(d2)/365
}
rho_call(50,0.5,45,0.06,0.25,0)
```

```
## [1] 0.04628839
```

       
 
  
       
  
 
  
