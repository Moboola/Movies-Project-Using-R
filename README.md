# Movies-Project-Using-R
Within this repo, you will find the dataset generated through R programming, accompanied by my Power BI dashboard. Employing my analytical expertise, I meticulously navigated the data in an end-to-end assignment utilizing R programming in conjunction with Power BI.
You can find the link:-

![image](https://github.com/Moboola/Movies-Project-Using-R/assets/142215138/4027d081-dc4a-40ed-ae39-41b408224b75)

# Load Data

# Load library

install.packages("tidyverse")


# Check data types

str(hmps)
dim(hmps)
summary(hmps)

# Check for missing values
colSums(is.na(hmps))

# Drop missing values

hmps_cleaned <- hmps <- na.omit(hmps)

dim(hmps_cleaned)

# Check for duplicates and remove them

duplicated_rows <- duplicated(hmps_cleaned)

# check the count of duplicated data

duplicated_count <- table(duplicated_rows)
print(duplicated_count)

# round off vales to 2 places
# round off values for profitability to 2 places
hmps_cleaned$Profitability <- round(hmps_cleaned$Profitability,digit=2)

# round off values for Worldwide.Gross   to 2 places
hmps_cleaned$Worldwide.Gross <- round(hmps_cleaned$Worldwide.Gross,digit=2)
View(hmps_cleaned)

#Check for outliers using a boxplot

library(ggplot2)

#barplot(hmps_cleaned$Audience..score..,main="Bar Chart - hmps_cleaned$Profitability",labels=names(hmps_cleaned$Audience..score..),col=c("lightblue", "brown", "blue"))


ggplot(hmps_cleaned, aes(x=Profitability, y=Worldwide.Gross)) + geom_boxplot(outlier.colour = "red", outlier.shape = 1)+ scale_x_continuous(labels = scales::comma)+coord_cartesian(ylim = c(0, 1000))

# Remove outliers in 'Profitability'

Q1 <- quantile(hmps_cleaned$Profitability, .25)

Q3 <- quantile(hmps_cleaned$Profitability, .75)

IQR <- IQR(hmps_cleaned$Profitability)

no_outliers <- subset(hmps_cleaned, hmps_cleaned$Profitability> (Q1 - 1.5*IQR) & hmps_cleaned$Profitability< (Q3 + 1.5*IQR)) 


dim(no_outliers)


#Remove outliers in Worldwide.Gross

Q1 <- quantile(no_outliers$Worldwide.Gross, .25)

Q3 <- quantile(no_outliers$Worldwide.Gross, .75)

IQR <- IQR(no_outliers$Worldwide.Gross)
