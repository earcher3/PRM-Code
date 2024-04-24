setwd("C:/Users/EKArc/OneDrive/Documents/2024 Spring Classes/Predictive Risk Modeling")
War= read.csv("WarBaseData.csv",header=TRUE,sep=",")
names(War)
attach(War)

numrow = nrow(War)
party_dummy = matrix(nrow = numrow, ncol = 1)
for(i in 1:numrow){
  if(Polly.Party[i] == "D"){
    party_dummy[i,] = 1
  } else if(Polly.Party[i] == "S"){
    party_dummy[i,] = 2
  } else {
    party_dummy[i,] = 0
  }
}
head(party_dummy)
colnames(party_dummy) = "party_dummy"
War$Polly.Party = party_dummy

baselm = lm(Current.Enlistment ~ . - State - Active.Duty.Military.Members - Total.Reserves, data= War)
summary(baselm)
