# t-est_clean_data_monthly
Python code to obtain monthly data of Mexican government bond yields with maturities from 1 to 120 months.

Data comes from Valmer's "Curva Nominal 'Zero'". Valmer uses information of Mexican government bond yields from Cetes (zero coupon bonds
with maturities less than one year) and Bonos M (coupond bonds with maturities greater than one year) to construct daily yield curves with
maturities ranging from 1 to 10,920 days:

  - To obtain zero rates for maturities greater than one year, Valmer uses the method of bootstrapping.
  - To interpolate, Valmer uses the method of cublc interpolation with lineal estimation of slopes.
  - To extrapolate, Valmer uses de method of constant forward rates.

For more information you can consult Valmer's methodology contained in the repository (spanish only): 1_1_1_2_Nominales_Cero.pdf


For this project, we use end-of-month's yield curve as the observed one in that month. We calculate yields using the following algorithm:
 - Use the implied discount curve to calculate the zero coupond yield using the following formula:
    # y = -100*log(p)/(1/360)
    # y = yield
    # p = discount factor
    
  - We calculate yields for maturities ranging from 1 to 120 months wehre 1 month is equivalent to 30.4375 days.
    # To obtain yields with maturities of multiples of 30.4375 days, we linearly interpolate using the nearest lower and upper observations.
