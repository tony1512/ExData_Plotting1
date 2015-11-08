# ExData_Plotting1
Introduction

This assignment uses data from the UC Irvine Machine Learning Repository, a popular repository for machine learning datasets. In particular, we will be using the "Individual household electric power consumption Data Set" which I have made available on the course web site:

Dataset: Electric power consumption [20Mb]

Description: Measurements of electric power consumption in one household with a one-minute sampling rate over a period of almost 4 years. Different electrical quantities and some sub-metering values are available.

The following descriptions of the 9 variables in the dataset are taken from the UCI web site:

Date: Date in format dd/mm/yyyy
Time: time in format hh:mm:ss
Global_active_power: household global minute-averaged active power (in kilowatt)
Global_reactive_power: household global minute-averaged reactive power (in kilowatt)
Voltage: minute-averaged voltage (in volt)
Global_intensity: household global minute-averaged current intensity (in ampere)
Sub_metering_1: energy sub-metering No. 1 (in watt-hour of active energy). It corresponds to the kitchen, containing mainly a dishwasher, an oven and a microwave (hot plates are not electric but gas powered).
Sub_metering_2: energy sub-metering No. 2 (in watt-hour of active energy). It corresponds to the laundry room, containing a washing-machine, a tumble-drier, a refrigerator and a light.
Sub_metering_3: energy sub-metering No. 3 (in watt-hour of active energy). It corresponds to an electric water-heater and an air-conditioner.

getwd()
#find the directory

select_data <- subset(mydata, Date== "1/2/2007" | Date== "2/2/2007")
#select data from the database

> dim(select_data)
[1] 2880    9

global_active_power <- as.numeric(select_data$Global_active_power)

hist(global_active_power, col="red", main="Global Active Power", xlab="Global Active Power (kilowatts)")

dev.copy(png, file="plot1.png", height=480, width=480)
dev.off()

#Save the file

datetime <- paste(as.Date(select_data$Date), select_data$Time)
select_data$Datetime <- as.POSIXct(datetime)
plot(global_active_power~select_data$Datetime, type="l",ylab="Global Active Power (kilowatts)", xlab="")
png("plot2.png", width=480, height=480)
dev.copy(png, file="plot2.png", height=480, width=480)
dev.off()

subMetering1 <- as.numeric(workdata$Sub_metering_1)
subMetering2 <- as.numeric(workdata$Sub_metering_2)
subMetering3 <- as.numeric(workdata$Sub_metering_3)

png("plot3.png", width=480, height=480)

# List min and max of sub metering variables to define proper range
l_min<-c(min(subMetering1),min(subMetering2),min(subMetering3))
l_max<-c(max(subMetering1),max(subMetering2),max(subMetering3))

# Plot the chart without axis
plot(globalActivePower, type="n", ylim=range(l_min,l_max), axes=F, ann=T, xlab=NA,ylab='Energy sub metering')
# Add x axis with three ticks and three labels

axis(1, at=c(0,nrow(workdata)/2,nrow(workdata)),labels=c('Thu','Fri','Sat'))
# Add y axis
axis(2)
# Box it up
box()

# Add lines for each sub metering variable
lines(workdata$Sub_metering_1)
lines(workdata$Sub_metering_2,col='Red')
lines(workdata$Sub_metering_3,col='Blue')

# Add legend
legend("topright", legend = c("Sub_metering_1", "Sub_metering_2","Sub_metering_3"),col=c('Black','Red','Blue'),lty=c(1,1,1))

# Close device
dev.off()

# Define two rows and two columns with adjusted margins for better reading
par(mfrow=c(2,2),mar=c(4,4,1,1))

# Chart 1
plot(globalActivePower, type="l", ylim=range(globalActivePower), axes=F, ann=T, xlab=NA,ylab='Global Active Power')
axis(1, at=c(0,nrow(workdata)/2,nrow(workdata)),labels=c('Thu','Fri','Sat'))
axis(2)
box()

# Chart 2
plot(workdata$Voltage, type="l", ylim=range(workdata$Voltage), axes=F, ann=T, xlab='datetime',ylab='Voltage')
axis(1, at=c(0,nrow(workdata)/2,nrow(workdata)),labels=c('Thu','Fri','Sat'))
axis(2)
box()

# Chart 3
plot(workdata$Global_active_power, type="n", ylim=range(l_min,l_max), axes=F, ann=T, xlab=NA,ylab='Energy sub metering')
axis(1, at=c(0,nrow(workdata)/2,nrow(workdata)),labels=c('Thu','Fri','Sat'))
axis(2)
box()
lines(subMetering1)
lines(subMetering2,col='Red')
lines(subMetering3,col='Blue')
legend("topright", legend = c("Sub_metering_1", "Sub_metering_2","Sub_metering_3"),col=c('Black','Red','Blue'),lty=c(1,1,1),cex=0.7)

# Chart 4
plot(workdata$Global_reactive_power, type="l", ylim=range(workdata$Global_reactive_power), axes=F, ann=T, xlab='datetime',ylab='Global_reactive_power')
axis(1, at=c(0,nrow(workdata)/2,nrow(workdata)),labels=c('Thu','Fri','Sat'))
axis(2)
box()

# Close device
dev.off()
