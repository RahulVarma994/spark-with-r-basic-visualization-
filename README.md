# spark-with-r-basic-visualization-

hotttnesss <- track_metadata_tbl %>%
# Select artist_hotttnesss
select(artist_hotttnesss) %>%
# Binarize to is_hottt_or_nottt
ft_binarizer("artist_hotttnesss",
"is_hottt_or_nottt",
threshold = 0.5) %>%
# Collect the result
collect() %>%
# Convert is_hottt_or_nottt to logical
mutate(is_hottt_or_nottt = as.logical(is_hottt_or_nottt))
# Draw a barplot of is_hottt_or_nottt
ggplot(hotttnesss,
aes(is_hottt_or_nottt)) +
geom_bar()

##########################
# track_metadata_tbl, decades, decade_labels have been pre-defined
track_metadata_tbl
decades
decade_labels

hotttnesss_over_time <- track_metadata_tbl %>%
# Select artist_hotttnesss and year
select(artist_hotttnesss, year) %>%
# Convert year to numeric
mutate(year = as.numeric(year)) %>%
# Bucketize year to decade using decades vector
ft_bucketizer("year", "decade", splits = decades) %>%
# Collect the result
collect() %>%
# Convert decade to factor using decade_labels
mutate(decade = factor(decade, labels = decade_labels))
# Draw a boxplot of artist_hotttnesss by decade
ggplot(hotttnesss_over_time, aes(decade, artist_hotttnesss)) + geom_boxplot()
 
