# ExData_Plotting1

getwd()
#find the directory


> select_data <- subset(mydata, Date== "1/2/2007" | Date== "2/2/2007")
#select data from the database

> dim(select_data)
[1] 2880    9

> global_active_power <- as.numeric(select_data$Global_active_power)

> hist(global_active_power, col="red", main="Global Active Power", xlab="Global Active Power (kilowatts)")


> dev.copy(png, file="plot1.png", height=480, width=480)
> dev.off()
#Save the file


> datetime <- paste(as.Date(select_data$Date), select_data$Time)
> select_data$Datetime <- as.POSIXct(datetime)
> plot(global_active_power~select_data$Datetime, type="l",ylab="Global Active Power (kilowatts)", xlab="")
> png("plot2.png", width=480, height=480)
> dev.copy(png, file="plot2.png", height=480, width=480)
> dev.off()




>subMetering1 <- as.numeric(workdata$Sub_metering_1)
>subMetering2 <- as.numeric(workdata$Sub_metering_2)
>subMetering3 <- as.numeric(workdata$Sub_metering_3)



>png("plot3.png", width=480, height=480)

# List min and max of sub metering variables to define proper range
>l_min<-c(min(subMetering1),min(subMetering2),min(subMetering3))
>l_max<-c(max(subMetering1),max(subMetering2),max(subMetering3))
>
# Plot the chart without axis
>plot(globalActivePower, type="n", ylim=range(l_min,l_max), axes=F, ann=T, xlab=NA,ylab='Energy sub metering')
># Add x axis with three ticks and three labels
>axis(1, at=c(0,nrow(workdata)/2,nrow(workdata)),labels=c('Thu','Fri','Sat'))
# Add y axis
>axis(2)
# Box it up
>box()

# Add lines for each sub metering variable
>lines(workdata$Sub_metering_1)
>lines(workdata$Sub_metering_2,col='Red')
>lines(workdata$Sub_metering_3,col='Blue')

# Add legend
+legend("topright", legend = c("Sub_metering_1", "Sub_metering_2","Sub_metering_3"),col=c('Black','Red','Blue'),lty=c(1,1,1))

# Close device
>dev.off()



# Define two rows and two columns with adjusted margins for better reading
>par(mfrow=c(2,2),mar=c(4,4,1,1))

# Chart 1
>plot(globalActivePower, type="l", ylim=range(globalActivePower), axes=F, ann=T, xlab=NA,ylab='Global Active Power')
>axis(1, at=c(0,nrow(workdata)/2,nrow(workdata)),labels=c('Thu','Fri','Sat'))
>axis(2)
>box()

# Chart 2
>plot(workdata$Voltage, type="l", ylim=range(workdata$Voltage), axes=F, ann=T, xlab='datetime',ylab='Voltage')
>axis(1, at=c(0,nrow(workdata)/2,nrow(workdata)),labels=c('Thu','Fri','Sat'))
>axis(2)
>box()

# Chart 3
>plot(workdata$Global_active_power, type="n", ylim=range(l_min,l_max), axes=F, ann=T, xlab=NA,ylab='Energy sub metering')
>axis(1, at=c(0,nrow(workdata)/2,nrow(workdata)),labels=c('Thu','Fri','Sat'))
>axis(2)
>box()
>lines(subMetering1)
>lines(subMetering2,col='Red')
>lines(subMetering3,col='Blue')
>legend("topright", legend = c("Sub_metering_1", >"Sub_metering_2","Sub_metering_3"),col=c('Black','Red','Blue'),lty=c(1,1,1),cex=0.7)

# Chart 4
>plot(workdata$Global_reactive_power, type="l", ylim=range(workdata$Global_reactive_power), axes=F, ann=T, >xlab='datetime',ylab='Global_reactive_power')
>axis(1, at=c(0,nrow(workdata)/2,nrow(workdata)),labels=c('Thu','Fri','Sat'))
>axis(2)
>box()

# Close device
>dev.off()
