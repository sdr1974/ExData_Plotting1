# Course Project 1

## Getting and Cleaning the Data

### Getting the Data

```
library(dplyr)
library(tidyr)
file <-  unzip(zipfile = "./power.consumption.zip", files = NULL, list = FALSE, overwrite = TRUE)
electric.power <- read.delim("./household_power_consumption.txt", header = TRUE, sep = ";", dec = ".",
                             na.strings = "?", colClasses = c("character", "character", "numeric", "numeric", "numeric", 
                                                              "numeric", "numeric", "numeric", "numeric"))
```                                                              

### Extracting Data From 2007-02-01 to 2007-02-02

```
electric.power$Date <- as.Date(electric.power$Date, "%d/%m/%Y")
electric.power <- filter(electric.power, Date >= as.Date("2007-02-01") & Date <= as.Date ("2007-02-02"))
electric.power[complete.cases(electric.power), ]
```

### Creating Date/Time

```
Date.Time <- paste(electric.power$Date, electric.power$Time)
Date.Time <- as.POSIXct(Date.Time)
```

### Adding Date/Time in the DF

```
electric.power <- cbind(Date.Time, electric.power) 
electric.power <- select(electric.power, -Date, -Time)
```

## Plot 1

```
hist(electric.power$Global_active_power, col = "red", main = "Global Active Power", xlab = "Global Active Power (kilowatts)")
```

![plot1.png](https://github.com/sdr1974/ExData_Plotting1/blob/master/plot1.png)

**Copying the Plot**
```
dev.copy(png, file = "plot1.png", width = 480, height = 480)
dev.off()
```

## Plot 2

```
plot(electric.power$Global_active_power~electric.power$Date.Time, type = "l", xlab = "", ylab = "Global Active Power (kilowatts)")
```

![plot2.png](https://github.com/sdr1974/ExData_Plotting1/blob/master/plot2.png)

**Copying the Plot**
```
dev.copy(png, file = "plot2.png", width = 480, height = 480)
dev.off()
```

## Plot 3

```
plot(electric.power$Date.Time, electric.power$Sub_metering_1,  type = "l", xlab = "", ylab = "Energy sub Metering")
lines(electric.power$Date.Time, electric.power$Sub_metering_2, type = "l", col = "red")
lines(electric.power$Date.Time, electric.power$Sub_metering_3, type = "l", col = "blue")
legend("topright", col = c("black", "red", "blue"), lwd = c(2,2,2), c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"))
```
![plot3.png](https://github.com/sdr1974/ExData_Plotting1/blob/master/plot3.png)

**Copying the Plot**
```
dev.copy(png, file = "plot3.png", width = 480, height = 480)
dev.off()
```
## Plot 4

```
par(mfrow = c(2, 2))
plot(electric.power$Global_active_power~electric.power$Date.Time, type = "l", xlab = "", ylab = "Global Active Power (kilowatts)")
plot(electric.power$Date.Time, electric.power$Voltage, type = "l", xlab = "datetime", ylab = "voltage")
plot(electric.power$Date.Time, electric.power$Sub_metering_1,  type = "l", xlab = "", ylab = "Energy sub Metering")
lines(electric.power$Date.Time, electric.power$Sub_metering_2, type = "l", col = "red")
lines(electric.power$Date.Time, electric.power$Sub_metering_3, type = "l", col = "blue")
legend("topright", col = c("black", "red", "blue"), lwd = c(2,2,2), c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"))
plot(electric.power$Date.Time, electric.power$Global_reactive_power, type = "l", xlab = "datetime", ylab = "Global Reactive Power")
```
![plot4.png](https://github.com/sdr1974/ExData_Plotting1/blob/master/plot4.png)

**Copying the Plot**
```
dev.copy(png, file = "plot4.png", width = 480, height = 480)
dev.off()
```
