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
