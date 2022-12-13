# GallupBinaryResponsesQuestions
It contains all the Gallup World Poll questions with binary responses (e.g. Yes/No, Support/Not Support, Agree/Disagree, Satisfied/Dissatisfied, etc.).

This is the code for getting the table if you have the raw Gallup data(imported as `gallupExt` here):

```
Gallup.Binary <- lapply(colnames(gallupExt), 
                       function(var){
    if (identical(get_values(gallupExt[, var]), c(1, 2, 3, 4)) &&
        (grepl("(DK(\b|\\W))|(((Do not)|dont|don\\?t) know\\W{0,1}$)|refuse|\\(RF\\)|(\\(none\\))", get_labels(gallupExt[, var])[3], ignore.case = T)| 
         grepl("(DK(\b|\\W))|(((Do not)|dont|don\\?t) know\\W{0,1}$)|refuse|\\(RF\\)|(\\(none\\))", get_labels(gallupExt[, var])[4], ignore.case = T)))
        return(
            data.frame(matrix(
                c(var,
                  get_label(gallupExt[, var]),
                  get_labels(gallupExt[, var])),
                1)))
}) %>% 
                bind_rows

colnames(Gallup.Binary) <- c("QTag", "Short Text", "RESPONSE VALUE = 1 for BinaryQ", 
                             "RESPONSE VALUE = 2 for BinaryQ", "RESPONSE VALUE = 3 for BinaryQ", 
                             "RESPONSE VALUE = 4 for BinaryQ")
```
