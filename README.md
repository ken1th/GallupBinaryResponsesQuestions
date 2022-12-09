# GallupBinaryResponsesQuestions
It contains all the Gallup World Poll questions with binary responses (e.g. Yes/No, Support/Not Support, Agree/Disagree, Satisfied/Dissatisfied, etc.).

This is the code for getting the table if you have the raw Gallup data(imported as `gallupExt` here):
```
GallupBinary <- lapply(colnames(gallupExt), 
                       function(var){
    if (identical(get_values(gallupExt[, var]), c(1, 2, 3, 4)) &&
        (get_labels(gallupExt[, var])[3] %in% "(DK)" | 
         get_labels(gallupExt[, var])[4] %in% "(Refused)"))
        return(
            data.frame(matrix(
                c(var,
                  get_label(gallupExt[, var]),
                  get_labels(gallupExt[, var])),
                1)))
}) %>% 
                bind_rows

colnames(GallupBinary) <- c("QTAG", "SHORT TEXT", "RESPONSE VALUE = 1", 
                            "RESPONSE VALUE = 2", "RESPONSE VALUE = 3", "RESPONSE VALUE = 4")

write.csv(GallupBinary, "GallupBinaryQuestions.csv", row.names = F)
```
