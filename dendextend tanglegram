#if (!require(dendextend)) install.packages(dendextend);
rm(list=ls())
setwd("C:/Users/Administrator/Desktop/dendextend_demo")

library(dendextend)
library(dplyr)
library(DECIPHER)
library(ggplot2)

#load source data
dend1 <- ReadDendrogram("dend1.newick", internalLabels = FALSE)
dend2 <- ReadDendrogram("dend2.newick", internalLabels = FALSE)

#read the clade/color data
tip_metadata <- read.csv("taxon_color.csv", sep="\t", header=TRUE,check.names=FALSE, stringsAsFactor=F)

#set label colors trees
virus_lab <- labels(dend1)
virus_lab <- tip_metadata$clade
virus_lab <- as.factor(virus_lab)
levels(virus_lab) <- 1:length(levels(virus_lab))
labels_colors(dend1) <- virus_lab

# Stepwise untangle one tree compared to another
dend2_corrected <- untangle_step_rotate_1side(dend1, dend2)[[1]]

#Create a dendrogram with color branches) 
dl <- dendlist(color_branches(dend1, clusters = as.numeric(virus_lab),col=levels(virus_lab)), 
               color_branches(dend2_corrected, clusters = as.numeric(virus_lab), col=levels(virus_lab)))

#Print entanglement
dl %>% entanglement # lower is bette

tanglegram(dl, 
           main_left = "Tree_1", 
           main_right = "Tree_2",
           color_lines = as.numeric(virus_lab),
           lwd = .5, 
           axes = TRUE,
           type = "r",
           remove_nodePar = TRUE, 
           highlight_distinct_edges = FALSE, 
           highlight_branches_lwd=FALSE, 
           common_subtrees_color_lines = FALSE, 
           edge.lwd = .8,
           lab.cex = .1, 
           faster = FALSE)
