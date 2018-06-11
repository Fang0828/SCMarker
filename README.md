# SCMarker

SCMarker is about marker selection on single cell RNA sequenceing data. This package implement the marker selection algorithm developed by Fang Wang. It provides the user with tools for generating features to further clustering. This is done based on two hypotheses. One is that gene should follow bi/multi-modal distribution in a mixed cell population if it is a marker of a specific cell type. The second is that genes which are the markers of the same cell type should co-express in the same cells.



Marker selection
---------------------
The three main functions for this package are `ModalFilter()`, `GeneFilter()` and `getMarker()`. The first does the initial filter based on the least expressed number of genes(cells) and whether the gene is unimodal distribution. The second takes the output of `ModalFilter()` and filtered the genes which are unimodal distribution and express in more than maxexp cells. The last takes the output of `geneFilter()` and selects the final markers based on gene pairs which are mutual maximally co-expressed in cells.



Usage
----------------------
```
Download SCMarker_1.0.tar.gz
```

```R
install.packages("SCMarker_1.0.tar.gz",repos=NULL,type="source")
data(melanoma)
melanoma1=as.matrix(melanoma[,2:dim(melanoma)[2]])
row.names(melanoma1)=melanoma[,1]
filterres=ModalFilter(data=melanoma1,geneK=10,cellK=10,width=2,cutoff=2)
filterres=GeneFilter(filterres=filterres,maxexp=dim(filterres$data)[2]*0.8)
filterres=getMarker(filterres=filterres,MNN=200,MNNindex=20)
filterres$marker
```