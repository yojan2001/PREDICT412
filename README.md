PREDICT412
## variable names
## customer_ID  shopping_pt	record_type	day	time	state	location	group_size	homeowner	car_age	car_value	
## risk_factor	age_oldest	age_youngest	married_couple	C_previous	duration_previous	A	B	C	D	E	F	G	cost

setwd("C:\\Users\\abo586\\Documents\\Dropbox\\PREDICT\\PREDICT 412\\Team")
library(Hmisc)
library(car)
library(psych)
library(MMST)
library(lattice)
library(corrplot)
library(ellipse)
library(xtable)
library(PerformanceAnalytics)
library(dplyr)
library(caret)
library(ROCR)
library(randomForest)
library(nnet)
library(ggplot2)
library(tables)
library(reporttools)
library(data.table)


train=read.csv("train.csv")
test=read.csv("test_v2.csv")


#######################
###data manipulation###
#######################
smalltrain=train[1:1000,] #create a smaller subset in train for easier sample computation tests
train$plan=paste0(train$A, train$B, train$C, train$D, train$E, train$F, train$G)#concatenate plan options
#train$customer_ID = as.factor(train$customer_ID)#turn customerID into a factor 
#train$record_type = as.factor(train$record_type)#turn record type into a factor
#train$location = as.factor(train$location)
#train$car_value= as.factor(train$car_value)
#train$group_size=as.factor(train$group_size)
#train$homeowner = as.factor(train$homeowner)
#train$risk_factor = as.factor(train$risk_factor)
#train$married_couple = as.factor(train$married_couple)

#new time variable for train set
#train$time <- strptime(as.character(train$time),"%H:%M")
#train2 <- data.table(train)
#clust3 <- function(x) cutree(hclust(dist(as.numeric(x))),k=3)
#system.time(tc <- train2[,clust3(time),by=customer_ID])
#train2$ctime <- tc$V1
#train$timecat <- train2$ctime
#as.factor(train$timecat)
#train2[1:25,c("customer_ID","time","ctime"),with=FALSE]

#newtime <- function(x){(as.numeric(strptime(as.character(x),"%H:%M")-strptime("00:00","%H:%M")))}


smalltest=test[1:1000,] #create a smaller subset in train for easier sample computation tests
test$plan=paste0(test$A, test$B, test$C, test$D, test$E, test$F, test$G)#concatenate plan options
#test$customer_ID = as.factor(test$customer_ID)#turn customerID into a factor 
#test$record_type = as.factor(test$record_type)#turn record type into a factor
#test$location = as.factor(test$location)
#test$car_value= as.factor(test$car_value)
#test$group_size=as.factor(test$group_size)
#test$homeowner = as.factor(test$homeowner)
#test$risk_factor = as.factor(test$risk_factor)
#test$married_couple = as.factor(test$married_couple)



##################
###DESCRIPTIVES###
##################
sapply(train,class) #class of entire dataset
sapply(test,class) 
sapply(train, function(x) length(unique(x)))# anonymous function to return unique values for each variable in the data frame
sapply(train,class) #class of entire dataset
sapply(test, function(x) length(unique(x)))
uniquetrain=unique(train$customer_ID)#creates a factor with unique values on the customer_ID variable

##check for missing values
##missing values
sapply(train, function(x) sum(is.na(x)))
sapply(test, function(x) sum(is.na(x)))


#histogram: shopping points by record type - whether they purchased or not
with(train, hist(shopping_pt))
with(test, hist(shopping_pt))





==========
