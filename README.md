# Getting-and-Cleaning-Data-Course-Project

run_analysis<-function (){
  # List of activities
  activities<-read.table("C:/Users/Bernard/Desktop/Coursera2/Course 3_Getting and Cleaning Data/ProgrammingAssignement1/activity_labels.txt")
  
  #List of wanted features
  features2<-read.table("C:/Users/Bernard/Desktop/Coursera2/Course 3_Getting and Cleaning Data/ProgrammingAssignement1/features.txt")
  wantedfeatures<-grep(".*mean.*|.*std.*",features2[,2])
  features[,2] <- as.character(features[,2])
  wantedfeaturesNames<-features2[wantedfeatures,2]
  wantedfeaturesNames = gsub('-mean', 'Mean', wantedfeaturesNames)
  wantedfeaturesNames = gsub('-std', 'Std', wantedfeaturesNames)
  wantedfeaturesNames <- gsub('[-()]', '', wantedfeaturesNames)
  
  #Load the train and test data
  train2<-read.table("C:/Users/Bernard/Desktop/Coursera2/Course 3_Getting and Cleaning Data/ProgrammingAssignement1/train/x_train.txt")[,wantedfeatures]
  subject2<-read.table("C:/Users/Bernard/Desktop/Coursera2/Course 3_Getting and Cleaning Data/ProgrammingAssignement1/train/subject_train.txt")
  activities2<-read.table("C:/Users/Bernard/Desktop/Coursera2/Course 3_Getting and Cleaning Data/ProgrammingAssignement1/train/y_train.txt")
  train2 <- cbind(subject2, activities2, train2)
  
  test3<-read.table("C:/Users/Bernard/Desktop/Coursera2/Course 3_Getting and Cleaning Data/ProgrammingAssignement1/test/x_test.txt")[,wantedfeatures]
  subject3<-read.table("C:/Users/Bernard/Desktop/Coursera2/Course 3_Getting and Cleaning Data/ProgrammingAssignement1/test/subject_test.txt")
  activities3<-read.table("C:/Users/Bernard/Desktop/Coursera2/Course 3_Getting and Cleaning Data/ProgrammingAssignement1/test/y_test.txt")
  test3 <- cbind(subject3, activities3, test3)
  
  #Merge the dataset
  allData<-rbind(train2, test3)
  colnames(allData) <- c("subject", "activity", wantedfeaturesNames)
}
