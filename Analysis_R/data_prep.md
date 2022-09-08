# Prepare experiment data

`setwd("/Users/oni/Documents/cognitive_biases_on annotation_task/Data/Batch2/data")`

```r
library(readxl)
library(tidyr)
library(dplyr)
library(ggstatsplot)
#library(rstatix)
library(ggplot2)
```

Import survey data

```r
data_survey <- read_excel("data.xlsx")
# Remove incomplete cases (with no exp data)
data_survey <- data_survey[complete.cases(data_survey[ , "annotationexp:1"]),]
```

---

Import experiment data

```r

# Check if data has the expected nrow
for (i in 1:nrow(data_survey)){
filename = paste("../Raw_data/", data_survey[i ,"annotationexp:1"][[1]] , sep="")
subdata <- read.table(filename, header = FALSE, sep = " ", dec = ".",fill = TRUE)
subdata <- subdata[complete.cases(subdata[ , 2:9]),]
y[i] <- nrow(subdata)
}

# Check all data is complete
~~if (nrow(subdata)==280) {
y[i] <- 1
} else {
y[i] <- 2
}~~

```

Import data in a big dataframe

```r

df_raw = data.frame()

for (i in 1:nrow(data_survey)){
filename = paste("experiment_data/", data_survey[i ,"annotationexp:1"][[1]] , sep="")
subdata <- read.table(filename, header = FALSE, sep = " ", dec = ".",fill = TRUE)
subdata <- subdata[complete.cases(subdata[ , 2:9]),]
subdata$subid <- data_survey$endcode[i]

if (i==1) {
df_raw <- rbind(df_raw,subdata)
} else {
common <- intersect(colnames(df_raw), colnames(subdata))
df_raw <- rbind(df_raw[common],subdata[common])
}
}

df_raw$bias <- gsub("_.*$", "", df_raw$V1)

colnames(df_raw) <- c("img_name", "strRT", "RT", "strRN", "Rel12", "str_conf", "raw_CONF" ,"CONF" ,"strl_ans_rel", "Relevant", "Var_bias","R_LAB", "Level", "stim_lab", "subid", "bias")

```

Set correct answers

```r
(df_raw <- df_raw %>%
  tidyr::unite(
    data = .,
    col = "Correct",
    R_LAB,
    Relevant,
    sep = "_",
    remove = FALSE
  ))

df_raw["Correct"][df_raw["Correct"] == "NRE_0"] <- "1"
df_raw["Correct"][df_raw["Correct"] == "REL_1"] <- "1"

df_raw["Correct"][df_raw["Correct"] == "NRE_1"] <- "0"
df_raw["Correct"][df_raw["Correct"] == "REL_0"] <- "0"

```
