# Prepare experiment data


```r
library(readxl)
library(tidyr)
library(dplyr)
library(ggstatsplot)
#library(rstatix)
library(ggplot2)
```

## Bandwagon Effect

```r
# Get Bandwagon and no bias

data_BE_raw <- df_raw[(df_raw$bias== c("BE","NO")),]

# Factor condition

data_BE_raw$Condition <- data_BE_raw$Var_bias

data_BE_raw["Condition"][data_BE_raw["Condition"] == "0"] <- "Low"
data_BE_raw["Condition"][data_BE_raw["Condition"] == "1"] <- "Low"
data_BE_raw["Condition"][data_BE_raw["Condition"] == "2"] <- "Low"
data_BE_raw["Condition"][data_BE_raw["Condition"] == "3"] <- "Low"

data_BE_raw["Condition"][data_BE_raw["Condition"] == "4"] <- "Equal"
data_BE_raw["Condition"][data_BE_raw["Condition"] == "5"] <- "Equal"
data_BE_raw["Condition"][data_BE_raw["Condition"] == "6"] <- "Equal"

data_BE_raw["Condition"][data_BE_raw["Condition"] == "7"] <- "High"
data_BE_raw["Condition"][data_BE_raw["Condition"] == "8"] <- "High"
data_BE_raw["Condition"][data_BE_raw["Condition"] == "9"] <- "High"
data_BE_raw["Condition"][data_BE_raw["Condition"] == "10"] <- "High"

data_BE_raw$Condition[is.na(data_BE_raw$Condition)] = "NO"

data_BE_raw$Correct <- as.numeric(data_BE_raw$Correct)

# Aggregate for lmer

data_BE_agg = aggregate(data_BE_raw,
                by = list(data_BE_raw$subid, data_BE_raw$Condition, data_BE_raw$Level),
                FUN = mean)

   data_BE_agg$subid <- data_BE_agg$Group.1
   data_BE_agg$Condition <- data_BE_agg$Group.2
   data_BE_agg$Level <- data_BE_agg$Group.3


 # Run lmer

  model_lmer<-lmer(Correct~factor(Condition)*factor(Level) + (1|subid), data=data_BE_agg)

     # Type III effects

      Anova(model_lmer)

     # Post-hoc

      emmeans(model_lmer,pairwise ~ Condition|Level, type = "response", , adjust = "fdr")

# Same for confidence level

  model_lmer<-lmer(CONF~factor(Condition)*factor(Level) + (1|subid), data=data_BE_agg)

      Anova(model_lmer)

      emmeans(model_lmer,pairwise ~ Level, type = "response", , adjust = "fdr")


# Same for reaction time

  model_lmer<-lmer(RT~factor(Condition)*factor(Level) + (1|subid), data=data_BE_agg)

      Anova(model_lmer)

```

### Decoy Effect

```r

# Get Decoy data

DE_DF <- df_raw[(df_raw$bias=="DE"),]

DE_DF$Correct <- as.numeric(DE_DF$Correct)

DE_agg = aggregate(DE_DF,
                by = list(DE_DF$subid, DE_DF$Level, DE_DF$Var_bias),
                FUN = mean)
 DE_agg$subid <- DE_agg$Group.1
 DE_agg$Level <- DE_agg$Group.2
 DE_agg$Var_bias <- DE_agg$Group.3


# Run models and posthoc

model_lmerDE<-lmer(Correct~factor(Var_bias)*factor(Level) + (1|subid), data=DE_agg)

  Anova(model_lmerDE)

  emmeans(model_lmerDE,pairwise ~ Var_bias, type = "response", , adjust = "none")



model_lmerDE<-lmer(CONF~factor(Var_bias)*factor(Level) + (1|subid), data=DE_agg)

  Anova(model_lmerDE)



model_lmerDE<-lmer(RT~factor(Var_bias)*factor(Level) + (1|subid), data=DE_agg)

  Anova(model_lmerDE)

```

# Ambiguity Effect

```r

# Get AE and no bias data

data_AE_raw <- df_raw[(df_raw$bias== c("AE","NO")),]

    data_AE_raw$Condition <- data_AE_raw$Var_bias

    data_AE_raw["Condition"][data_AE_raw["Condition"] == "1"] <- "Info"
    data_AE_raw["Condition"][data_AE_raw["Condition"] == "2"] <- "Unknwon"
    data_AE_raw$Condition[is.na(data_AE_raw$Condition)] = "NO"

    data_AE_raw$Correct <- as.numeric(data_AE_raw$Correct)

    data_AE_agg = aggregate(data_AE_raw,
                    by = list(data_AE_raw$subid, data_AE_raw$Condition, data_AE_raw$Level),
                    FUN = mean)

     data_AE_agg$subid <- data_AE_agg$Group.1
     data_AE_agg$Condition <- data_AE_agg$Group.2
     data_AE_agg$Level <- data_AE_agg$Group.3

# Run models and posthoc

model_lmer<-lmer(Correct~factor(Condition)*factor(Level) + (1|subid), data=data_AE_agg)

    Anova(model_lmer)

    emmeans(model_lmer,pairwise ~ Level, type = "response", , adjust = "none")

model_lmer<-lmer(CONF~factor(Condition)*factor(Level) + (1|subid), data=data_BE_agg)

    Anova(model_lmer)

    emmeans(model_lmer,pairwise ~ Level, type = "response", , adjust = "none")


```
