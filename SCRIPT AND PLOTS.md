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







