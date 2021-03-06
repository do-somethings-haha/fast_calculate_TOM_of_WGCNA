# Optimize weighted gene co-expression network analysis: fast calculate unsigned Topological Overlap Matrix from unsigned or signed Adjacency Matrix

<h1>Introduction</h1>

  &nbsp;&nbsp;&nbsp;&nbsp; Biomolecular networks are usually scale-free hierarchical networks. The weighted gene co-expression network analysis (WGCNA) package in R language treats gene co-expression networks as undirected scale-free hierarchical weighted networks. WGCNA uses an Adjacency Matrix to store a network, next calculates the Topological Overlap Matrix (TOM), and then gets the modules (sub-networks), each module corresponds to a certain biological function. The most time-consuming step of WGCNA is to calculate TOM from the Adjacency Matrix in a single thread. This paper changes the single-threaded algorithm of the TOM to a multi-threaded algorithm (only for the calculation of commonly used unsigned or signed Adjacency Matrix to unsigned TOM). This paper uses Rcpp to make R call a C++ function, then C++ uses OpenMP to open multiple threads, and calculates TOM from the Adjacency Matrix. On Shared-memory MultiProcessor systems, the calculation time decreases as the number of CPU cores increases. The algorithm of this paper can promote the application of WGCNA on large data sets, and help other research fields to find sub-networks in undirected scale-free hierarchical weighted networks.<br/><br/>
  &nbsp;&nbsp;&nbsp;&nbsp; The codes here can run on Linux and Windows systems. It’s better to use a CPU cooler with a fast fan speed to avoid the CPU running at reduced frequency due to high temperature.

<h1>Usage of codes</h1>
Before starting the following steps, please install two packages in the R language 
install.packages( c("Rcpp" , "RcppArmadillo") )

<h2>If you want to analyze the transcriptome data with WGCNA and the codes here<h2>

<h3>Step 1: Put the source code files of R and C++ in the working directory of R and install R packages</h3>
  &nbsp;&nbsp;&nbsp;&nbsp; The file path of the R working directory should contain only English letters, numbers, and underscores. Then use the following code to install two packages in R language.
  <pre>install.packages( c("Rcpp" , "RcppArmadillo") )</pre>

<h3>Step 2: Run the R code you just copied instead of WGCNA's TOMsimilarity function</h3>
  &nbsp;&nbsp;&nbsp;&nbsp; You need to use the WGCNA package to calculate the unsigned or signed Adjacency Matrix from the expression matrix. "unsigned" is the default value of the parameter named type of the "adjacency" function in the WGCNA. Then you can run the R codes that you downloaded from here. Next you will get the TOM with TOMtype="unsigned" and TOMDenom="min". TOMtype="unsigned" and TOMDenom="min" are the default parameters in the "TOMsimilarity" function of the WGCNA.

<br/><br/>
<h2>If you want to analyze data from other research fields<h2>
<h3></h3>
  &nbsp;&nbsp;&nbsp;&nbsp; If other research fields need to find sub-networks from undirected scale-free hierarchical weighted networks, you can refer to the C++ header files prepared for other research fields here. This header file defines a function that can use a symmetric Adjacency Matrix to calculate an unsigned Topological Overlap Matrix. Then you can use the Topological Overlap Matrix to divide the sub-networks.

<h1>References</h1>

Details about Weighted gene co-expression network analysis(WGCNA) of R language:  <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;  https://horvath.genetics.ucla.edu/html/CoexpressionNetwork/Rpackages/WGCNA/   <br/>
Details about the usage of original TOMsimilarity() function in WGCNA   <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;  https://horvath.genetics.ucla.edu/html/CoexpressionNetwork/Rpackages/WGCNA/Tutorials/FemaleLiver-02-networkConstr-man.pdf  <br/>
Details about mathematical formulas of the Topological Overlap Matrix (TOM): <br/>
  &nbsp;&nbsp;&nbsp;&nbsp;  https://horvath.genetics.ucla.edu/html/CoexpressionNetwork/Rpackages/WGCNA/TechnicalReports/index.html

