rm(list=ls())
library(Rcpp)
library(readxl)
data <- read_excel("C:/A_Proyecto de grado/Base de datos del Proyecto/data.xlsx")
View(data)


summary(data)
library(smoother)
library(tseries)
library(forecast)
library(psych)

#### Estadística descriptiva

###Promedio
mean(data$EXCAT)
mean(data$EXCAD)
mean(data$HACUC)
mean(data$ABIMD)
mean(data$PQDMUSA)
mean(data$PQDMWORLD)
mean(data$HIMUSAD)
mean(data$TRAUSA)

###Desviaci?n est?ndar
sd(data$EXCAT)
sd(data$EXCAD)
sd(data$HACUC)
sd(data$ABIMD)
sd(data$PQDMUSA)
sd(data$PQDMWORLD)
sd(data$HIMUSAD)
sd(data$TRAUSA)

###Calculo de Curtosis (Pmero hay que intarlar paquete psych)

kurtosi(data$EXCAT)
kurtosi(data$EXCAD)
kurtosi(data$HACUC)
kurtosi(data$ABIMD)
kurtosi(data$PQDMUSA)
kurtosi(data$PQDMWORLD)
kurtosi(data$HIMUSAD)
kurtosi(data$TRAUSA)

### Coeficiente de asimetria

skew(data$EXCAT)
skew(data$EXCAD)
skew(data$HACUC)
skew(data$ABIMD)
skew(data$PQDMUSA)
skew(data$PQDMWORLD)
skew(data$HIMUSAD)
skew(data$TRAUSA)


## Análisis de la serie de tiempo mediante SUAVIZAMIENTO

## Descomposici?n de la serie y gr?ficas ####
inds <- 2005:2022

library(ggplot2)
library(tidyr)
library(dplyr)
library(tidyverse)
require(smooth)

### EXCAT SUAVIZAMIENTO


EXCAT2= ts(data$EXCAT, 
           start = 2005,
           frequency = 1)
ts.plot(EXCAT2, v=2015)
lines(SMA(EXCAT2 , n=2), col="red")
abline(v=2012)


A_EXCAT<-sma(EXCAT2 , order =3, h=5)

A_EXCAT$forecast

A_EXCAT$fitted
plot(forecast(A_EXCAT, h=5, interval = "empirical"))


##Excad suavizamiento
EXCAD2= ts(data$EXCAD, 
           start = 2005,
           frequency = 1)
ts.plot(EXCAD2, v=2015)
lines(SMA(EXCAD2 , n=2), col="blue")
abline(v=2012)

A_EXCAD<-sma(EXCAD2 , order =3 , h=5)

A_EXCAD$forecast

A_EXCAD$fitted
plot(forecast(A_EXCAD, h=5, interval = "empirical"))



##HACUC Suavizamiento
HACUC2= ts(data$HACUC, 
           start = 2005,
           frequency = 1)
ts.plot(HACUC2, v=2015)
lines(SMA(HACUC2 , n=2), col="red")
abline(v=2012)

A_HACUC<-sma(HACUC2 , order =3, h=5)

A_HACUC$forecast

A_HACUC$fitted
plot(forecast(A_HACUC, h=5, interval = "empirical"))


##ABIMD SUAVIZAMIENTO
ABIMD2= ts(data$ABIMD, 
           start = 2005,
           frequency = 1)
ts.plot(ABIMD2, v=2015)
lines(SMA(ABIMD2 , n=2), col="blue")
abline(v=2012)

A_ABIMD2<-sma(ABIMD2 , order =3, h=5)

A_ABIMD2$forecast

A_ABIMD2$fitted
plot(forecast(A_ABIMD2, h=5, interval = "empirical"))


##PQDMUSA SUAVIZAMIENTO
PQDMUSA2= ts(data$PQDMUSA, 
           start = 2005,
           frequency = 1)
ts.plot(PQDMUSA2, v=2015)
lines(SMA(PQDMUSA2 , n=2), col="red")
abline(v=2012)


A_PQDMUSA<-sma(PQDMUSA2 , order =3, h=5)

A_PQDMUSA$forecast

A_PQDMUSA$fitted
plot(forecast(A_PQDMUSA, h=5, interval = "empirical"))



##PQDMWORLD
PQDMWORLD2= ts(data$PQDMWORLD, 
           start = 2005,
           frequency = 1)
ts.plot(PQDMWORLD2, v=2015)
lines(SMA(PQDMWORLD2 , n=2), col="blue")
abline(v=2012)

A_PQDMWORLD<-sma(PQDMWORLD2 , order =3, h=5)

A_PQDMWORLD$forecast

A_PQDMWORLD$fitted
plot(forecast(A_PQDMWORLD, h=5, interval = "empirical"))

##HIMUSAD Suvaizamiento
HIMUSAD2= ts(data$HIMUSAD, 
           start = 2005,
           frequency = 1)
ts.plot(HIMUSAD2, v=2015)
lines(SMA(HIMUSAD2 , n=2), col="red")
abline(v=2012)

A_HIMUSAD<-sma(HIMUSAD2 , order =3, h=5)

A_HIMUSAD$forecast

A_HIMUSAD$fitted
plot(forecast(A_HIMUSAD, h=5, interval = "empirical"))

##TRAUSA Suavizamiento

TRAUSA2= ts(data$TRAUSA, 
           start = 2005,
           frequency = 1)
ts.plot(TRAUSA2, v=2015)
lines(SMA(TRAUSA2 , n=2), col="blue")
abline(v=2012)

A_TRAUSA<-sma(TRAUSA2 , order =3, h=5)

A_TRAUSA$forecast

A_TRAUSA$fitted
plot(forecast(A_TRAUSA, h=5, interval = "empirical"))



##ESTACIONARIDAD
adf.test(log(EXCAT2))
adf.test(log(EXCAD2))
adf.test(log(HACUC2))
adf.test(log(ABIMD2))
adf.test(log(PQDMUSA2))
adf.test(log(PQDMWORLD2))
adf.test(log(HIMUSAD2))
adf.test(log(TRAUSA2))


D_EXCAT2=diff(EXCAT2, differences=4)
adf.test(D_EXCAT2)
par(mfrow=c(1,2))
auto.arima(EXCAT2)
acf(EXCAT2)
acf(EXCAT2, type="partial")


D_EXCAD2=diff(log(EXCAD2), differences=3)
adf.test(D_EXCAD2)
par(mfrow=c(1,2))
auto.arima(EXCAD2)
acf(EXCAD2)
acf(EXCAD2, type="partial")


D_HACUC2=diff(log(HACUC2), differences=6)
adf.test(D_HACUC2)
par(mfrow=c(1,2))
auto.arima(HACUC2)
acf(HACUC2)
acf(HACUC2, type="partial")

D_ABIMD2=diff(log(ABIMD2), differences=2)
adf.test(D_ABIMD2)
par(mfrow=c(1,2))
auto.arima(ABIMD2)
acf(ABIMD2)
acf(ABIMD2, type="partial")

D_PQDMUSA2=diff(log(PQDMUSA2), differences=1)
adf.test(D_PQDMUSA2)
par(mfrow=c(1,2))
auto.arima(PQDMUSA2)
acf(PQDMUSA2)
acf(PQDMUSA2, type="partial")

D_PQDMWORLD2=diff(log(PQDMWORLD2), differences=2)
adf.test(D_PQDMWORLD2)
par(mfrow=c(1,2))
auto.arima(PQDMWORLD2)
acf(PQDMWORLD2)
acf(PQDMWORLD2, type="partial")

D_HIMUSAD2=diff(log(HIMUSAD2), differences=4)
adf.test(D_HIMUSAD2)
par(mfrow=c(1,2))
auto.arima(HIMUSAD2)
acf(HIMUSAD2)
acf(HIMUSAD2, type="partial")

D_TRAUSA2=diff(log(TRAUSA2), differences=10)
adf.test(D_TRAUSA2)
par(mfrow=c(1,2))
auto.arima(TRAUSA2)
acf(TRAUSA2)
acf(TRAUSA2, type="partial")

###MODELOS

####
##Modelo EXCAT

modelo1_EXCAT=arima(EXCAT2,c(1,4,1))
plot(EXCAT2)

modelo2_EXCAT=arima(EXCAT2,c(2,4,3))
modelo3_EXCAT=arima(EXCAT2,c(2,4,2))
modelo4_EXCAT=auto.arima(EXCAT2)

residuals(modelo1_EXCAT)
checkresiduals (modelo1_EXCAT)
plot(residuals(modelo1_EXCAT))

residuals(modelo2_EXCAT)
checkresiduals (modelo2_EXCAT)
plot(residuals(modelo2_EXCAT))

residuals(modelo3_EXCAT)
checkresiduals (modelo3_EXCAT)
plot(residuals(modelo3_EXCAT))

residuals(modelo4_EXCAT)
checkresiduals (modelo4_EXCAT)
plot(residuals(modelo4_EXCAT))

AIC(modelo1_EXCAT)
AIC(modelo2_EXCAT)
AIC(modelo3_EXCAT)
AIC(modelo4_EXCAT)
##Mejor modelo el 1




##Modelo EXCAD
modelo1_EXCAD=arima(EXCAD2,c(0,3,0))
modelo2_EXCAD=arima(EXCAD2,c(3,3,3))
modelo3_EXCAD=arima(EXCAD2,c(2,3,2))
modelo4_EXCAD=auto.arima(EXCAD2)

residuals(modelo1_EXCAD)
checkresiduals (modelo1_EXCAD)
plot(residuals(modelo1_EXCAD))

residuals(modelo2_EXCAD)
checkresiduals (modelo2_EXCAD)
plot(residuals(modelo2_EXCAD))

residuals(modelo3_EXCAD)
checkresiduals (modelo3_EXCAD)
plot(residuals(modelo3_EXCAD))

residuals(modelo4_EXCAD)
checkresiduals (modelo4_EXCAD)
plot(residuals(modelo4_EXCAD))

AIC(modelo1_EXCAD)
AIC(modelo2_EXCAD)
AIC(modelo3_EXCAD)
AIC(modelo4_EXCAD)
##Mejor modelo el 3


##Modelo HACUC
modelo1_HACUC=arima(HACUC2,c(1,6,2))
modelo2_HACUC=arima(HACUC2,c(0,6,0))
modelo3_HACUC=arima(HACUC2,c(3,6,3))
modelo4_HACUC=auto.arima(HACUC2)

residuals(modelo1_HACUC)
checkresiduals (modelo1_HACUC)
plot(residuals(modelo1_HACUC))

residuals(modelo2_HACUC)
checkresiduals (modelo2_HACUC)
plot(residuals(modelo2_HACUC))

residuals(modelo3_HACUC)
checkresiduals (modelo3_HACUC)
plot(residuals(modelo3_HACUC))

residuals(modelo4_HACUC)
checkresiduals (modelo4_HACUC)
plot(residuals(modelo4_HACUC))

AIC(modelo1_HACUC)
AIC(modelo2_HACUC)
AIC(modelo3_HACUC)
AIC(modelo4_HACUC)
## Mejor modelo el 1


##Modelo ABIMD
modelo1_ABIMD=arima(ABIMD2,c(4,2,5))
modelo2_ABIMD=arima(ABIMD2,c(2,2,2))
modelo3_ABIMD=arima(ABIMD2,c(5,2,4))
modelo4_ABIMD=auto.arima(ABIMD2)

residuals(modelo1_ABIMD)
checkresiduals (modelo1_ABIMD)
plot(residuals(modelo1_ABIMD))

residuals(modelo2_ABIMD)
checkresiduals (modelo2_ABIMD)
plot(residuals(modelo2_ABIMD))

residuals(modelo3_ABIMD)
checkresiduals (modelo3_ABIMD)
plot(residuals(modelo3_ABIMD))

residuals(modelo4_ABIMD)
checkresiduals (modelo4_ABIMD)
plot(residuals(modelo4_ABIMD))

AIC(modelo1_ABIMD)
AIC(modelo2_ABIMD)
AIC(modelo3_ABIMD)
AIC(modelo4_ABIMD)
##Mejor modelo el 2


##Modelo PQDMUSA
modelo1_PQDMUSA=arima(PQDMUSA2,c(1,1,3))
modelo2_PQDMUSA=arima(PQDMUSA2,c(2,1,2))
modelo3_PQDMUSA=arima(PQDMUSA2,c(4,1,4))
modelo4_PQDMUSA=auto.arima(PQDMUSA2)

residuals(modelo1_PQDMUSA)
checkresiduals (modelo1_PQDMUSA)
plot(residuals(modelo1_PQDMUSA))

residuals(modelo2_PQDMUSA)
checkresiduals (modelo2_PQDMUSA)
plot(residuals(modelo2_PQDMUSA))

residuals(modelo3_PQDMUSA)
checkresiduals (modelo3_PQDMUSA)
plot(residuals(modelo3_PQDMUSA))

residuals(modelo4_PQDMUSA)
checkresiduals (modelo4_PQDMUSA)
plot(residuals(modelo4_PQDMUSA))

AIC(modelo1_PQDMUSA)
AIC(modelo2_PQDMUSA)
AIC(modelo3_PQDMUSA)
AIC(modelo4_PQDMUSA)
##Mejor modelo el 4


##Modelo PQDMWORLD
modelo1_PQDMWORLD=arima(PQDMWORLD2,c(1,2,1))
modelo2_PQDMWORLD=arima(PQDMWORLD2,c(4,2,4))
modelo3_PQDMWORLD=arima(PQDMWORLD2,c(2,2,1))
modelo4_PQDMWORLD=auto.arima(PQDMWORLD2)

residuals(modelo1_PQDMWORLD)
checkresiduals (modelo1_PQDMWORLD)
plot(residuals(modelo1_PQDMWORLD))

residuals(modelo2_PQDMWORLD)
checkresiduals (modelo2_PQDMWORLD)
plot(residuals(modelo2_PQDMWORLD))

residuals(modelo3_PQDMWORLD)
checkresiduals (modelo3_PQDMWORLD)
plot(residuals(modelo3_PQDMWORLD))

residuals(modelo4_PQDMWORLD)
checkresiduals (modelo4_PQDMWORLD)
plot(residuals(modelo4_PQDMWORLD))

AIC(modelo1_PQDMWORLD)
AIC(modelo2_PQDMWORLD)
AIC(modelo3_PQDMWORLD)
AIC(modelo4_PQDMWORLD)
##Mejor modelo el 3


##Modelo HIMUSAD
modelo1_HIMUSAD=arima(HIMUSAD2,c(1,4,1))
modelo2_HIMUSAD=arima(HIMUSAD2,c(2,4,4))
modelo3_HIMUSAD=arima(HIMUSAD2,c(3,4,3))
modelo4_HIMUSAD=auto.arima(HIMUSAD2)

residuals(modelo1_HIMUSAD)
checkresiduals (modelo1_HIMUSAD)
plot(residuals(modelo1_HIMUSAD))

residuals(modelo2_HIMUSAD)
checkresiduals (modelo2_HIMUSAD)
plot(residuals(modelo2_HIMUSAD))

residuals(modelo3_HIMUSAD)
checkresiduals (modelo3_HIMUSAD)
plot(residuals(modelo3_HIMUSAD))

residuals(modelo4_HIMUSAD)
checkresiduals (modelo4_HIMUSAD)
plot(residuals(modelo4_HIMUSAD))

AIC(modelo1_HIMUSAD)
AIC(modelo2_HIMUSAD)
AIC(modelo3_HIMUSAD)
AIC(modelo4_HIMUSAD)
##Mejor modelo el 1



##Modelo TRAUSA
modelo1_TRAUSA=arima(TRAUSA2,c(1,10,4))
modelo2_TRAUSA=arima(TRAUSA2,c(1,10,5))
modelo3_TRAUSA=arima(TRAUSA2,c(1,10,3))
modelo4_TRAUSA=auto.arima(TRAUSA2)

residuals(modelo1_TRAUSA)
checkresiduals (modelo1_TRAUSA)
plot(residuals(modelo1_TRAUSA))

residuals(modelo2_TRAUSA)
checkresiduals (modelo2_TRAUSA)
plot(residuals(modelo2_TRAUSA))

residuals(modelo3_TRAUSA)
checkresiduals (modelo3_TRAUSA)
plot(residuals(modelo3_TRAUSA))

residuals(modelo4_TRAUSA)
checkresiduals (modelo4_TRAUSA)
plot(residuals(modelo4_TRAUSA))

AIC(modelo1_TRAUSA)
AIC(modelo2_TRAUSA)
AIC(modelo3_TRAUSA)
AIC(modelo4_TRAUSA)
 ###Mejor modelo el 3



###Predicciones 

# EXCAT Mejor modelo = 1

predict_EXCAT=forecast(modelo1_EXCAT, h=5,level=c(80,95,99))

plot(predict_EXCAT)

# EXCAD Mejor modelo = 3

predict_EXCAD=forecast(modelo3_EXCAD, h=5,level=c(80,95,99))

plot(predict_EXCAD)

# HACUC Mejor modelo = 1

predict_HACUC=forecast(modelo1_HACUC, h=5,level=c(80,95,99))

plot(predict_HACUC)

# ABIMD Mejor modelo = 2

predict_ABIMD=forecast(modelo2_ABIMD, h=5,level=c(80,95,99))

plot(predict_ABIMD)

# PQDMUSA Mejor modelo = 4

predict_PQDMUSA=forecast(modelo4_PQDMUSA, h=5,level=c(80,95,99))

plot(predict_PQDMUSA)

# PQDMWORLD Mejor modelo = 3

predict_PQDMWORLD=forecast(modelo3_PQDMWORLD, h=5,level=c(80,95,99))

plot(predict_PQDMWORLD)

# HIMUSAD Mejor modelo = 1

predict_HIMUSAD=forecast(modelo1_HIMUSAD, h=5,level=c(80,95,99))

plot(predict_HIMUSAD)

# TRAUSA Mejor modelo = 3

predict_TRAUSA=forecast(modelo3_TRAUSA, h=5,level=c(80,95,99))

plot(predict_TRAUSA)




###### Regresión discontinua 
library(readxl)
data_disc <- read_excel("C:/A_Proyecto de grado/Base de datos del Proyecto/data_disc.xlsx")
View(data_disc)

library(tidyverse)
library(haven)
library(estimatr)



lm_1 <- lm_robust(EXCAT ~ TIME, data = data_disc, clusters = TLC)
summary(lm_1)
lm_2 <- lm_robust(EXCAD ~ TIME, data = data_disc, clusters = TLC)
summary(lm_2)
lm_3 <- lm_robust(HACUC ~ TIME, data = data_disc, clusters = TLC)
summary(lm_3)
lm_4 <- lm_robust(ABIMD ~ TIME, data = data_disc, clusters = TLC)
summary(lm_4)
lm_5 <- lm_robust(PQDMUSA ~ TIME, data = data_disc, clusters = TLC)
summary(lm_5)
lm_6 <- lm_robust(PQDMWORLD ~ TIME, data = data_disc, clusters = TLC)
summary(lm_6)
lm_7 <- lm_robust(HIMUSAD ~ TIME, data = data_disc, clusters = TLC)
summary(lm_7)
lm_8 <- lm_robust(TRAUSA ~ TIME, data = data_disc, clusters = TLC)
summary(lm_8)

modelsummary::msummary(list(lm_1,lm_2,lm_3,lm_4,lm_5,lm_6,lm_7,lm_8), stars = TRUE)

### EXCAT

ggplot(data_disc, aes(TIME, EXCAT)) +
  geom_point(aes(x = TIME, y = EXCAT), data = data_disc) +
  stat_smooth(aes(TIME, EXCAT, group = TLC), method = "lm", 
              formula = y ~ x + I(x^2)) +
  xlim(0,18) + ylim(100000,350000) +
  geom_vline(xintercept = 8)


### EXCAD

ggplot(data_disc, aes(TIME, EXCAD)) +
  geom_point(aes(x = TIME, y = EXCAD), data = data_disc) +
  stat_smooth(aes(TIME, EXCAD, group = TLC), method = "lm", 
              formula = y ~ x + I(x^2)) +
  xlim(0,18) + ylim(0,1780000) +
  geom_vline(xintercept = 8)


### HACUC

ggplot(data_disc, aes(TIME, HACUC)) +
  geom_point(aes(x = TIME, y = HACUC), data = data_disc) +
  stat_smooth(aes(TIME, HACUC, group = TLC), method = "lm", 
              formula = y ~ x + I(x^2)) +
  xlim(0,18) + ylim(750000,980000) +
  geom_vline(xintercept = 8)


### ABIMD

ggplot(data_disc, aes(TIME, ABIMD)) +
  geom_point(aes(x = TIME, y = ABIMD), data = data_disc) +
  stat_smooth(aes(TIME, ABIMD, group = TLC), method = "lm", 
              formula = y ~ x + I(x^2)) +
  xlim(0,18) + ylim(0,250000) +
  geom_vline(xintercept = 8)


### PQDMUSA

ggplot(data_disc, aes(TIME, PQDMUSA)) +
  geom_point(aes(x = TIME, y = PQDMUSA), data = data_disc) +
  stat_smooth(aes(TIME, PQDMUSA, group = TLC), method = "lm", 
              formula = y ~ x + I(x^2)) +
  xlim(0,18) + ylim(500000,1480000) +
  geom_vline(xintercept = 8)


### PQDMWORLD

ggplot(data_disc, aes(TIME, PQDMWORLD)) +
  geom_point(aes(x = TIME, y = PQDMWORLD), data = data_disc) +
  stat_smooth(aes(TIME, PQDMWORLD, group = TLC), method = "lm", 
              formula = y ~ x + I(x^2)) +
  xlim(0,18) + ylim(1000000,3350000) +
  geom_vline(xintercept = 8)


### HIMUSAD

ggplot(data_disc, aes(TIME, HIMUSAD)) +
  geom_point(aes(x = TIME, y = HIMUSAD), data = data_disc) +
  stat_smooth(aes(TIME, HIMUSAD, group = TLC), method = "lm", 
              formula = y ~ x + I(x^2)) +
  xlim(0,18) + ylim(0,70000) +
  geom_vline(xintercept = 8)


### TRAUSA

ggplot(data_disc, aes(TIME, TRAUSA)) +
  geom_point(aes(x = TIME, y = TRAUSA), data = data_disc) +
  stat_smooth(aes(TIME, TRAUSA, group = TLC), method = "lm", 
              formula = y ~ x + I(x^2)) +
  xlim(0,18) + ylim(0,44000) +
  geom_vline(xintercept = 8)





