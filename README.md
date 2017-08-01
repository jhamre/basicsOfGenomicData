# basicsOfGenomicData
Here we go through how to start navigating genomic data by using the Gollub gene expression dataset. 

Use Sweave. Go to "File" "New file" "R Sweave"  We will talk about font and headers later. 
\documentclass{article}

\begin{document}

<<>>=

#1)
#a)  
class(golub)

#b)
remove and rm can be used to remove objects. These can be specified successively as character strings, or in the character vector list, or through a combination of both. All objects thus specified will be removed.
sum returns the sum of all the values present in its arguments.
prod returns the product of all the values present in its arguments.
Generate regular sequences. seq is a standard generic with a default method.
 sd computes the standard deviation of the values in x. If na.rm is TRUE then missing values are removed before computation proceeds.
nrow computes the number of rows in a matrix
#c) 
grep can assist in finding the row index of the parameter of interest
apply is a function that allows the user to make computations on entire rows or columns
gl generate factors by specifying the pattern of their levels.  It is designed to indicate an experimental condition of a measurement or the group to which a patient belongs.
The function, library() is used to see which packages are currently installed on your operating system and can load data from package
source causes R to accept its input from the named file or URL or connection. Input is read and parsed from that file until the end of the file is reached, then the parsed expressions are evaluated sequentially in the chosen environment.
setwd() is used to set the working directory to dir.
The function history can be useful for collecting previously given commands.
str is used to compactly display the structure of an arbitrary R object

#2)
#a)     

 apply(gendat,2,sd)
   

#b)
 apply(gendat,1,sd)


#c) 

 sdexprsval <- apply(gendat, 1, sd)
 o <- order(sdexprsval, decreasing = TRUE)
 gendat[o,]
      
#d)
 gendat[o[1],]

#3)
#a) 
 golubRowMean <- apply(golub, 1, mean)
 golubRowMean

#b)
 o <- order(golubRowMean, decreasing = TRUE)
 golub[o,]  

#c)
 golub.gnames[o[1:3],3]
   

#d)
 golub.gnames[o[1:3],2]

#4)
#a)
golubRowSD <- apply(golub, 1, sd)

#b)
golubRowSDGreaterThan0.5 <- golub[golubRowSD>0.5,]

#c)
# I did this two ways

nrow(golubRowSDGreaterThan0.5)

 
 
sum(golubRowSD>0.5)



#5)
#a) 

 length(grep("oncogene",golub.gnames[,2], ignore.case = TRUE))


#b)  
 
 rowIndex <- grep("oncogene",golub.gnames[,2], ignore.case = TRUE)
 golubOncogenes <- golub[rowIndex,]
 golubOncogenes.gnames <- golub.gnames[rowIndex,]
 golubFactor <- factor(golub.cl,levels=0:1, labels= c("ALL","AML"))
 golubRowMeans <- apply(golubOncogenes[,golubFactor=="ALL"],1,mean)
 o <- order(golubRowMeans,decreasing=TRUE)
 golubOncogenes.gnames[o[1:3],2]

#c)
 golubRowMeans <- apply(golubOncogenes[,golubFactor=="AML"],1,mean)
 o <- order(golubRowMeans,decreasing=TRUE)
 golubOncogenes.gnames[o[1:3],2]

#d)
 x <- golubOncogenes.gnames[o[1:10],c(3,2)]
 colnames(x) <- c("probe ID","gene name")
 write.csv(x,file="C:/Users/John/Documents/R/golubOncogenes.csv")
 write.table(x,file="C:/Users/John/Documents/R/golubOncogenes.table", row.names=FALSE)

#6)
#a)
 gl(2,4)


#b)
 gl(5,3)

#c
 gl(3,5)


#7
#a  

 library(ALL); data(ALL)
 meanB1 <- apply(exprs(ALL[,ALL$BT=="B1"]),1, mean)
 o <- order(meanB1,decreasing=TRUE)

#b

 meanB1[o[1:3]]

@


\end{document}
