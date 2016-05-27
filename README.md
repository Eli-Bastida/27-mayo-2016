# 27-mayo-2016

## elejir una serie de tiempo
## aplicar la funcion auto.arima (p,q,d)
## apliquen funcion arima(p,q,d) con dos modelos diferentes al que genere la funcion auto arima
## generar los pronosticos de los 3 modelos
## generar una grafica con los valores reales y los valores ajustados  de los tres modelos
## genrar grafica con los valores ajustados y pronosticados en los tres modelos, numero de pronosticos -> 4

require (fpp)
bimbo <- read.csv ("C:\\Users\\SALA-C9\\Desktop\\bimbo.csv")
bimbots <- ts(bimbo[,2], start  = 2015, frequency = 52)
bimbots
mod1 <- auto.arima(bimbots, seasonal=FALSE)
mod1
mod2 <- Arima(bimbots, order= c(0, 0, 1))
mod3 <- Arima(bimbots, order= c(1, 0, 0))

pronos1<- forecast (mod1, h=6)
pronos2<- forecast (mod2, h=6)
pronos3<- forecast (mod3, h=6)

plot(pronos1, plot.conf=FALSE, ylab="Precios",
     xlab="semana, 2015", main="Precios de la Acción Bimbo", fcol="white", type="o")
lines(fitted(pronos2), col="blue", type="o")
lines(fitted(pronos3), col="red", type="o")
lines(pronos1$mean, col="green", type="o")
lines(pronos2$mean, col="blue", type="o")
lines(pronos3$mean, col="red", type="o")
legend("topleft",lty=5, col=c(1,"green","blue","red"), c("datos reales","mod1", "mod2", "mod3"),pch=1)

## fitted son los ajustes del pronostico y en pronostico$mean es el pronostico como tal
